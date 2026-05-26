# LlamaIndex LLMs Integration: Telnyx

[Telnyx](https://telnyx.com) provides an OpenAI-compatible Inference API for hosted LLMs including Llama, Qwen, DeepSeek, Kimi, and more.

This integration lets you use Telnyx-hosted models with LlamaIndex for chat, completion, streaming, and function calling workflows.

## Installation

```shell
pip install llama-index-llms-telnyx
```

## Setup

Get an API key from the [Telnyx Mission Control Portal](https://portal.telnyx.com/) and set it as an environment variable:

```bash
export TELNYX_API_KEY="your-api-key"
```

## Usage

### Basic Completion

```python
from llama_index.llms.telnyx import Telnyx

llm = Telnyx(model="meta-llama/Llama-3.3-70B-Instruct")

response = llm.complete("What is Telnyx?")
print(response)
```

### Chat

```python
from llama_index.core.llms import ChatMessage
from llama_index.llms.telnyx import Telnyx

llm = Telnyx(model="meta-llama/Llama-3.3-70B-Instruct")

messages = [
    ChatMessage(role="system", content="You are a helpful assistant."),
    ChatMessage(role="user", content="Explain WebRTC in simple terms."),
]
response = llm.chat(messages)
print(response)
```

### Streaming

```python
from llama_index.llms.telnyx import Telnyx

llm = Telnyx(model="meta-llama/Llama-3.3-70B-Instruct")

response = llm.stream_complete("What are the benefits of SIP trunking?")
for chunk in response:
    print(chunk.delta, end="")
```

### Async

```python
import asyncio
from llama_index.llms.telnyx import Telnyx

llm = Telnyx(model="meta-llama/Llama-3.3-70B-Instruct")

async def main():
    response = await llm.acomplete("What is WebRTC?")
    print(response)

asyncio.run(main())
```

## Configuration

| Parameter | Default | Description |
|-----------|---------|-------------|
| `model` | `meta-llama/Llama-3.3-70B-Instruct` | Model ID to use |
| `api_key` | `TELNYX_API_KEY` env var | Telnyx API key |
| `api_base` | `https://api.telnyx.com/v2/ai/openai` | API base URL (override via `TELNYX_API_BASE` env var) |
| `context_window` | `131072` | Context window size |
| `temperature` | `0.1` | Sampling temperature |
| `max_tokens` | `None` | Max tokens to generate |

## Available Models

Telnyx hosts a variety of models. Some popular options:

- `meta-llama/Llama-3.3-70B-Instruct`
- `meta-llama/Meta-Llama-3.1-8B-Instruct`
- `Qwen/Qwen3-235B-A22B`
- `moonshotai/Kimi-K2.6`
- `google/gemini-2.5-flash`

See the full list at [developers.telnyx.com/docs/inference/models](https://developers.telnyx.com/docs/inference/models).

## Resources

- [Telnyx AI Inference Docs](https://developers.telnyx.com/docs/inference/getting-started)
- [Telnyx Model Catalog](https://developers.telnyx.com/docs/inference/models)
- [Telnyx Portal](https://portal.telnyx.com/)
