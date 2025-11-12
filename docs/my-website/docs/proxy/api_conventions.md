import Image from '@theme/IdealImage';
# API Route Conventions

LiteLLM exposes both **OpenAI-compatible** and **LiteLLM-shortened** API routes.  
Both formats are valid and map to the same backend handler, but the `/v1/...` form is preferred for compatibility with OpenAI SDKs and client libraries.

---

## OpenAI-Compatible Routes

LiteLLM mirrors OpenAI’s REST API structure by supporting `/v1/...` paths for all endpoints.

These routes ensure that any OpenAI-compatible client can call your LiteLLM proxy **without any code changes**.

Example:
```bash
curl -X POST http://localhost:4000/v1/chat/completions \
  -H "Authorization: Bearer sk-test" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```

### Use `/v1/...` routes when:

- You’re integrating with **OpenAI SDKs** (Python, JS, etc.) or you are creating a **drop-in replacement** for OpenAI’s API.
- This format also works well when you’re building **production or shared environments**.

---

### Simplified LiteLLM Routes

LiteLLM also supports shorter aliases **without `/v1/`**.  
These are functionally identical to their `/v1/...` counterparts.

**Example:**
```bash
curl -X POST http://localhost:4000/chat/completions \
  -H "Authorization: Bearer sk-test" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```
This version works well for quick local testing, scripts, or debugging when you don’t need strict OpenAI path compatibility.

---

## Supported Endpoints

Both `/v1/...` and simplified forms are available for:

| Endpoint Type | OpenAI-Compatible | LiteLLM Alias |
|----------------|-------------------|---------------|
| Chat Completions | `/v1/chat/completions` | `/chat/completions` |
| Responses | `/v1/responses` | `/responses` |
| Completions (legacy) | `/v1/completions` | `/completions` |
| Embeddings | `/v1/embeddings` | `/embeddings` |
| Models | `/v1/models` | `/models` |

## Recommendation

For consistency across the docs and client integrations:

- Use `/v1/...` endpoints in examples and production code  
- Use the shorter aliases (`/chat/completions`, etc.) only for quick local tests

Note: If you see examples in the docs using `/chat/completions`, they will continue to work — but future documentation will standardize on the `/v1/...` form.
