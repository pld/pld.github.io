# Building a macOS UI for Ollama GenAI models in Rust

As we integrate AI dev tools into our teams, I experimented by writing a desktop app in a language I have never used relying on LLM code generation. I primarily used Claude via web and API through [aider](https://aider.chat/), with some help on more generic Rust questions from Gemini Advanced.

<img src="/assets/images/2025-03-07/screensage.png" alt="iced LLM UI in Rust" width="600px">

The main areas for human intervention where
- tweaking imports and syntax, that weren't worth the tokens,
- removing template code to get it to take user input,
- fixing the eventing to get messages sent from the UI to local the Ollama API,
- properly sharing state and using channels for realtime API to UI updates.

For some of these I'd manually intervene to get it on the right path then have it clean up. For others it probably would have figured it out with enough prompting direction, but it was easier for me to write the code than the prompts.

I have not tried this but if you're looking for a proper macOS LLM GUI, [Enchanted](https://github.com/gluonfield/enchanted) seems reasonable, but at time of writing last commit 4 months ago is a concern. Although it is Swift. I chose Rust with the goal of cross-platform, not sure if I will maintain this. See the code for a [MacOS UI for Ollama GenAI models in Rust](https://github.com/pld/turtles.)