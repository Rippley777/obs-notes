
# How to Run Cursor Against a Local AI Model

Below is a step-by-step guide for using [Cursor](https://www.cursor.so/) with a locally hosted model that mimics the OpenAI API. The main idea is to run a server that implements the same request/response endpoints as OpenAI, then point Cursor’s API calls to your local server instead of `api.openai.com`.

---

## 1. Install a Local Model Server

You’ll need a tool that can run a large language model (e.g., Llama 2, GPT-J, Vicuna) and expose an **OpenAI-compatible** API. A few popular options include:

- **[llama-cpp-python](https://github.com/abetlen/llama-cpp-python)**: Can be started with a `--api` flag to emulate `/v1/completions` or `/v1/chat/completions`.
- **[text-generation-webui (oobabooga)](https://github.com/oobabooga/text-generation-webui)**: Has a plugin or extension to provide an OpenAI-like API layer.
- **[OpenAI-API-compatible forks or servers](https://github.com/josStorer/OpenaiForward)**: Third-party projects that wrap local models with an OpenAI-like interface.

For example, using `llama-cpp-python`:

1. Install:
   ```bash
   pip install llama-cpp-python
```

Run a model with the built-in server:

`python -m llama_cpp.server \   --model /path/to/your/model/llama-2-7b.gguf \   --api`

This starts a local server (defaults to `http://localhost:8000`) that exposes routes similar to OpenAI’s API.


## 2. Set Environment Variables for Cursor

Cursor uses environment variables (or a config file) to determine how it calls the OpenAI API:

- **`OPENAI_API_KEY`**
- **`OPENAI_API_BASE`**

1. **API Base**: Point this to the local server URL (e.g., `http://localhost:8000/v1`).
2. **API Key**: Cursor expects some string, but your local server might not actually require it. You can set any placeholder.

On **macOS / Linux**, you might do:

```bash
export OPENAI_API_KEY="test-key"
export OPENAI_API_BASE="http://localhost:8000/v1"
```
## 3. Launch Cursor

With your local LLM server running and environment variables set, start Cursor. For example:

- On **macOS**, open from Finder/Spotlight or run:

```bash
open /Applications/Cursor.app
```

Cursor will read the environment variables and send its requests to your local model instead of the official OpenAI API.

---

## 4. Open Your Project in Cursor

1. **Open a Folder / Project**: In Cursor, select the codebase directory you want to work on.
2. **Let Cursor index your code**: It will parse files for references and context.
3. **Use the AI features**: Prompt Cursor for coding suggestions, refactors, or explanations in the chat panel or via inline suggestions.

All queries should now go to your locally hosted model via the API base you configured.

---

## 5. Troubleshooting

- **Mismatch Endpoints**: Ensure your local server listens on `/v1/chat/completions` or `/v1/completions` (whichever Cursor is using).
- **Server Logs**: Check the local server’s console for request/response info to confirm Cursor’s calls are reaching it.
- **Model Size & Hardware**: Large models can be resource-intensive. If performance is slow, try a smaller or more aggressively quantized model (e.g., Q4).
- **Context Window**: Your local model may have a smaller context window than GPT-4, so large code contexts or lengthy prompts might need splitting up.

That’s it! You can now use Cursor’s AI-assisted coding features entirely offline or self-hosted, ensuring privacy and control over your data and model.


To use Cursor with a local model and a supplied codebase, you can follow these steps:

1. Install Ollama, a tool for running AI models locally.
2. Pull a suitable model for coding tasks:


`ollama pull deepseek-r1:8b`

3. Set up a local server using Ollama or LM Studio to host your model13.
4. Use ngrok to create a public URL for your local server3.
5. Configure Cursor to use your local model:
    
    - Go to Cursor settings
    - Add the ngrok URL in the OpenAI override section
    - Append "/v1" to the end of the URL
    - Leave the API key field empty13
    
6. Enable codebase indexing in Cursor for better search accuracy[4](https://docs.cursor.com/chat/codebase).
7. Use "@codebase" or press Ctrl/Cmd + Enter when chatting to search your codebase[4](https://docs.cursor.com/chat/codebase).
8. To leverage your codebase, use commands like:text
    
    `@codebase How do plans work in this code?`
    Cursor will search your files and provide relevant information6.

This setup allows you to use Cursor with a local model while maintaining privacy and potentially reducing latency for code completion tasks[5](https://forum.cursor.com/t/add-support-for-ollama-natively/27291).




