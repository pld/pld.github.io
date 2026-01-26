---
layout: post
title: "wt: A Git Worktree Orchestrator for Parallel AI Agent Development"
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

Concurrent AI agent development introduces coordination problems when multiple agents modify the same repository. File conflicts occur when agents operate on overlapping code paths, and resolving these conflicts consumes agent context that would otherwise be applied to the task.

Git worktrees provide filesystem isolation while sharing repository state—each worktree maintains an independent working directory and branch reference without duplicating the object database. However, the native `git worktree` interface requires verbose commands, manual cleanup, and lacks primitives for managing multiple concurrent sessions.

**wt** is a CLI tool that addresses these limitations.

<img src="/assets/images/2026-01-26/demo.gif" alt="wt demo showing workspace creation and navigation" width="600" />

<h2>Overview</h2>

wt wraps git worktree operations in an interface designed for multi-agent workflows:

```bash
# Create an isolated workspace
wt new feature/auth

# Spawns a subshell with modified working directory and branch
# Shell prompt reflects workspace context
(wt:feature/auth) $ claude

# On completion, exit subshell and merge
exit
git merge feature/auth
```

Workspaces provide complete filesystem isolation. Each agent operates on an independent working directory, and changes integrate via standard git merge or rebase operations.

<h2>Workspace Management</h2>

wt provides both interactive and direct workspace access:

```bash
wt ls                  # Interactive picker (TUI) for workspace selection
wt use feature/auth    # Enter a specific workspace directly
wt which               # Display current workspace context
wt rm feature/auth     # Remove worktree and optionally delete branch
```

<h2>Tmux Session Management</h2>

wt integrates with tmux to coordinate multiple concurrent agent processes:

```bash
wt session new my-sprint
wt session add feature/auth
wt session add bugfix/header
wt session add feature/payments
```

Each workspace maps to a tmux window with a configurable pane layout: 2-pane (agent CLI + terminal) or 3-pane (agent + terminal + editor).

The `wt session watch` command displays agent activity state by monitoring pane output:

```
● feature/auth      (running)
○ bugfix/header     (idle)
● feature/payments  (running)
```

Activity detection uses output buffer analysis to distinguish active processing from prompt-waiting states.

<h2>Claude Code Integration</h2>

wt includes a `/do` skill for Claude Code that implements issue-driven workflows:

```bash
/do gh 123          # GitHub issue #123
/do sc 45678        # Shortcut story 45678
```

The skill executes the following operations:
<ol>
  <li>Fetch issue/story metadata from the respective API</li>
  <li>Create a worktree with a branch name derived from the issue identifier</li>
  <li>Populate agent context with issue description and acceptance criteria</li>
  <li>On task completion, create a commit with the issue reference in the message</li>
</ol>

<h2>Configuration</h2>

Configuration follows a precedence chain: CLI flags → repo-local `.wt.toml` → global `~/.wt/config.toml` → defaults.

```toml
# .wt.toml (repository root)
panes = 3
agent_cmd = "claude"
editor_cmd = "nvim"
```

Files listed under a `# wt copy` marker in `.gitignore` are symlinked from the main worktree into each spawned worktree:

```gitignore
# wt copy
.env
.env.local
credentials.json
```

This mechanism handles environment files and credentials that are gitignored but required at runtime.

<h2>Implementation</h2>

wt is implemented in Rust. The crate structure:

<ul>
  <li><strong>WorktreeManager</strong>: Wraps `git worktree` subcommands, maintains branch-to-directory mappings, handles cleanup of stale worktrees</li>
  <li><strong>TmuxManager</strong>: Interfaces with tmux via `tmux` CLI commands, monitors pane output buffers for activity detection</li>
  <li><strong>ShellEnvironment</strong>: Spawns subshells (bash, zsh, fish) with modified `$PWD` and environment variables reflecting workspace state</li>
  <li><strong>SessionState</strong>: Persists session metadata to JSON, reconciles with actual tmux state on load</li>
</ul>

Branch names containing forward slashes require path sanitization. Git permits `feature/auth` as a branch name, but using this directly as a directory path would create nested directories. wt normalizes slashes to double-dashes in directory names (`feature--auth`) while preserving the git ref name.

<h2>Installation</h2>

Pre-compiled binaries are available for macOS and Linux (x86_64, aarch64). Building from source:

```bash
git clone https://github.com/pld/wt
cd wt
cargo build --release
```

The binary includes an `install` subcommand that configures shell aliases and installs the Claude Code skill definition.

<h2>Discussion</h2>

Single-agent workflows operate adequately with standard git branching. Multi-agent parallelism introduces coordination overhead that scales with agent count: conflict resolution, context switching between agent sessions, and manual worktree lifecycle management.

wt reduces this overhead by mapping each agent to an isolated worktree and providing primitives for session orchestration. The tradeoff is an additional abstraction layer over git; the benefit is that agents operate independently until explicit merge points.

Source: <a href="https://github.com/pld/wt">github.com/pld/wt</a>
