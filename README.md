# intro_langchain

A hands-on, four-notebook walkthrough of the major concepts in LangChain v1, built from the official docs at [docs.langchain.com](https://docs.langchain.com/oss/python/langchain/overview).

The goal is not to memorize the API. It is to build the right mental model so that when you read someone else's LangChain code (or an agent framework built on top of it) you know what every piece is doing and why.

## What's inside

1. **`01_chat_models_and_messages.ipynb`** – The universal wrapper (`init_chat_model`), the four message types, and the three Runnable methods that show up everywhere: `invoke`, `stream`, `batch`.
2. **`02_prompts_and_chains.ipynb`** – `ChatPromptTemplate`, `MessagesPlaceholder`, output parsers, and the pipe operator (`prompt | model | parser`) that defines LCEL.
3. **`03_tools_and_structured_output.ipynb`** – The `@tool` decorator, `bind_tools`, the manual tool-call loop with `ToolMessage`, parallel tool calls, and `with_structured_output`.
4. **`04_putting_it_together.ipynb`** – Build a small agent two ways: hand-rolled with the loop from notebook 3, then again with `create_agent`. See what you save and what you give up.

Each notebook builds on the previous one. Run them in order the first time.

## Diagrams

The `diagrams/` folder has four `.drawio` files that explain how chat with an LLM actually works under the hood. Open them in [draw.io](https://app.diagrams.net/) (or the VS Code draw.io extension).

1. **`01_stateless_reality.drawio`** - one LLM call is fully stateless. Two back-to-back calls prove the model retains nothing between them.
2. **`02_chat_illusion_multiturn.drawio`** - how the chat illusion is built. Three turns side by side, with the message bundle growing each turn while the model itself stays stateless.
3. **`03_context_window_fills_up.drawio`** - why the bundle growing matters. Cost, latency, and the hard ceiling at the model's context window.
4. **`04_context_strategies.drawio`** - four ways production apps keep the bundle bounded: truncation, summarization, hybrid (summary + recent N), and vector retrieval.

If you only have time for one, read diagram 2. The whole rest of LangChain makes more sense once you see that picture.

## Setup

This project uses [`uv`](https://docs.astral.sh/uv/) for environment and dependency management. If you do not have it yet:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Then:

```bash
git clone https://github.com/fnusatvik07/intro_langchain.git
cd intro_langchain
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
cp .env.example .env
# edit .env and add at least one provider key
```

You only need one provider key (OpenAI, Anthropic, or Google). The notebooks default to OpenAI but the whole point of `init_chat_model` is that one line of code swaps the provider, so feel free to use whichever you have.

## A note on model names

The notebooks default to `gpt-4o-mini` because it is cheap and reliable for a tutorial. If you want to use a different model, change the one line at the top of each notebook. The rest of the code does not care.
