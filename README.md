# intro_langchain

A hands-on, four-notebook walkthrough of the major concepts in LangChain v1, built from the official docs at [docs.langchain.com](https://docs.langchain.com/oss/python/langchain/overview).

The goal is not to memorize the API. It is to build the right mental model so that when you read someone else's LangChain code (or an agent framework built on top of it) you know what every piece is doing and why.

## What's inside

1. **`01_chat_models_and_messages.ipynb`** – The universal wrapper (`init_chat_model`), the four message types, and the three Runnable methods that show up everywhere: `invoke`, `stream`, `batch`.
2. **`02_prompts_and_chains.ipynb`** – `ChatPromptTemplate`, `MessagesPlaceholder`, output parsers, and the pipe operator (`prompt | model | parser`) that defines LCEL.
3. **`03_tools_and_structured_output.ipynb`** – The `@tool` decorator, `bind_tools`, the manual tool-call loop with `ToolMessage`, parallel tool calls, and `with_structured_output`.
4. **`04_putting_it_together.ipynb`** – Build a small agent two ways: hand-rolled with the loop from notebook 3, then again with `create_agent`. See what you save and what you give up.

Each notebook builds on the previous one. Run them in order the first time.

## Setup

```bash
git clone https://github.com/fnusatvik07/intro_langchain.git
cd intro_langchain
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
# edit .env and add at least one provider key
```

You only need one provider key (OpenAI, Anthropic, or Google). The notebooks default to OpenAI but the whole point of `init_chat_model` is that one line of code swaps the provider, so feel free to use whichever you have.

## A note on model names

The notebooks default to `gpt-4o-mini` because it is cheap and reliable for a tutorial. If you want to use a different model, change the one line at the top of each notebook. The rest of the code does not care.
