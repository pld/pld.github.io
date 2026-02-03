---
layout: post
title: Testing voice AI agents with DSPy signatures and auto-healing graphs
categories:
- General
tags: []
author_id: 2
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

Platforms like Retell, VAPI, and LiveKit have made it straightforward to build phone-based AI assistants. But testing these agents before they talk to real customers remains painful: platform-specific formats, per-minute simulation charges, and no way to iterate on prompts without bleeding money.

voicetest is a test harness that solves this by running agent simulations with your own LLM keys. But beneath the surface, it's also a proving ground for something more interesting: auto-healing agent graphs that recover from test failures and optimize themselves using JIT synthetic data.

<img src="/assets/images/2026-02-03/cli-demo.gif" alt="voicetest CLI demo" width="600" />

<i>The interactive shell loads agents, configures models, and runs test simulations against DSPy-based judges.</i>

## The architecture: AgentGraph as IR

All platform formats (Retell CF, Retell LLM, VAPI, Bland, LiveKit, XLSForm) compile down to a unified intermediate representation called `AgentGraph`:

```python
class AgentGraph:
    nodes: dict[str, AgentNode]      # State-specific nodes
    entry_node_id: str               # Starting node
    source_type: str                 # Import source
    source_metadata: dict            # Platform-specific data
    default_model: str | None        # Model from import

class AgentNode:
    id: str
    state_prompt: str                # State-specific instructions
    tools: list[ToolDefinition]      # Available actions
    transitions: list[Transition]    # Edges to other states
```

This IR enables cross-platform testing and format conversion as a side effect. Import a Retell agent, test it, export to VAPI format. But more importantly, it gives us a structure we can reason about programmatically.

## DSPy signatures for structured LLM calls

Every LLM interaction in voicetest goes through DSPy signatures. This isn't just for cleaner code—it's the foundation for prompt optimization.

The **MetricJudgeSignature** handles LLM-as-judge evaluation:

```python
class MetricJudgeSignature(dspy.Signature):
    transcript: str = dspy.InputField()
    criterion: str = dspy.InputField()
    # Outputs
    score: float        # 0-1 continuous score
    reasoning: str      # Explanation
    confidence: float   # 0-1 confidence
```

Continuous scores (not binary pass/fail) are critical. A 0.65 and a 0.35 both "fail" a 0.7 threshold, but they represent very different agent behaviors. This granularity becomes training signal later.

The **UserSimSignature** generates realistic caller behavior:

```python
class UserSimSignature(dspy.Signature):
    persona: str = dspy.InputField()            # Identity/Goal/Personality
    conversation_history: str = dspy.InputField()
    current_agent_message: str = dspy.InputField()
    turn_number: int = dspy.InputField()
    # Outputs
    should_continue: bool
    message: str
    reasoning: str
```

Each graph node gets its own **StateModule** registered as a DSPy submodule:

```python
class ConversationModule(dspy.Module):
    def __init__(self, graph: AgentGraph):
        for node_id, node in graph.nodes.items():
            state_module = StateModule(node, graph)
            setattr(self, f"state_{node_id}", state_module)
            self._state_modules[node_id] = state_module
```

This structure means the entire agent graph is a single optimizable DSPy module. We can apply BootstrapFewShot or MIPROv2 to tune state transitions and response generation.

<img src="/assets/images/2026-02-03/web-demo.gif" alt="voicetest CLI demo" width="600" />

## Auto-healing the agent graph on test failures (coming soon)

When a test fails, the interesting question is: what should change? The failure might indicate a node prompt needs tweaking, or that the graph structure itself is wrong for the conversation flow.

The planned approach:

1. **Failure analysis**: Parse the transcript and judge output to identify where the agent went wrong. Was it a bad response in a specific state? A transition that fired incorrectly? A missing edge case?

2. **Mutation proposals**: Based on the failure mode, generate candidate fixes. For prompt issues, suggest revised state prompts. For structural problems, propose adding/removing transitions or splitting nodes.

3. **Validation**: Run the mutation against the failing test plus a regression suite. Only accept changes that fix the failure without breaking existing behavior.

This isn't implemented yet, but the infrastructure is there: the AgentGraph IR makes mutations straightforward, and the continuous metric scores give us a fitness function for evaluating changes.

## JIT synthetic data for optimization

DSPy optimizers like MIPROv2 need training examples. For voice agents, we generate these on demand:

1. **Test case expansion**: Each test case defines a persona and success criteria. We use the UserSimSignature to generate variations—different phrasings, edge cases, adversarial inputs.

2. **Trajectory mining**: Successful test runs become positive examples. Failed runs (with partial transcripts) become negative examples with the failure point annotated.

3. **Score-based filtering**: Because metrics produce continuous scores, we can select examples near decision boundaries (scores around the threshold) for maximum training signal.

The current implementation has the infrastructure:

```python
# Mock data generation for testing the optimization pipeline
simulator._mock_responses = [
    SimulatorResponse(message="Hello, I need help.", should_end=False),
    SimulatorResponse(message="Thanks, that's helpful.", should_end=False),
    SimulatorResponse(message="", should_end=True),
]
metric_judge._mock_results = [
    MetricResult(metric=m, score=0.9, passed=True)
    for m in test_case.metrics
]
```

The production version will generate real synthetic data by sampling from the UserSimSignature with temperature variations and persona mutations.

## Judgment pipeline

Three judges evaluate each transcript:

**Rule Judge** (deterministic, zero cost): substring includes/excludes, regex patterns. Fast pre-filter for obvious failures.

**Metric Judge** (LLM-based, semantic): evaluates each criterion with continuous scores. Per-metric threshold overrides enable fine-grained control. Global metrics (like HIPAA compliance) run on every test automatically.

**Flow Judge** (optional, informational): validates that node transitions made logical sense given the conversation. Uses the FlowValidationSignature:

```python
class FlowValidationSignature(dspy.Signature):
    graph_structure: str = dspy.InputField()
    transcript: str = dspy.InputField()
    nodes_visited: list[str] = dspy.InputField()
    # Outputs
    flow_valid: bool
    issues: list[str]
    reasoning: str
```

Flow issues don't fail tests but get tracked for debugging. A pattern of flow anomalies suggests the graph structure itself needs attention.

<img src="/assets/images/2026-02-03/web-demo.gif" alt="voicetest web UI" width="600" />

<i>The web UI visualizes agent graphs, manages test cases, and streams transcripts in real-time during execution.</i>

## CI/CD integration

Voice agents break in subtle ways. A prompt change that improves one scenario can regress another. voicetest runs in GitHub Actions:

```yaml
name: Voice Agent Tests
on:
  push:
    paths: ["agents/**"]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: astral-sh/setup-uv@v5
      - run: uv tool install voicetest
      - run: voicetest run --agent agents/receptionist.json --tests agents/tests.json --all
        env:
          OPENROUTER_API_KEY: ${{ secrets.OPENROUTER_API_KEY }}
```

Results persist to DuckDB, enabling queries across test history:

```sql
SELECT
    agents.name,
    COUNT(*) as total_runs,
    AVG(CASE WHEN results.passed THEN 1.0 ELSE 0.0 END) as pass_rate
FROM results
JOIN runs ON results.run_id = runs.id
JOIN agents ON runs.agent_id = agents.id
GROUP BY agents.name
```

## What's next

The current release handles the testing workflow: import agents, run simulations, evaluate with LLM judges, integrate with CI. The auto-healing and optimization features are in POC stage.

The roadmap:
- **v0.3**: JIT synthetic data generation from test case personas
- **v0.4**: DSPy optimization integration (MIPROv2 for state prompts)
- **v0.5**: Auto-healing graph mutations with regression protection

```bash
uv tool install voicetest
voicetest demo --serve
```

Code at <a href="https://github.com/voicetestdev/voicetest">github.com/voicetestdev/voicetest</a>. API docs at <a href="https://voicetest.dev/api/">voicetest.dev/api</a>. Apache 2.0 licensed.
