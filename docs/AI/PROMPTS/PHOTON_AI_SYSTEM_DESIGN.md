# 🧠 PHOTON_AI_SYSTEM_DESIGN.md

## 🔐 Future Considerations

Photon AI integration must be scalable, secure, and efficient. The following subsystems enable that vision.

---

### 🧮 Token Budgeting for Embedded OpenAPI Context

**Why**: LLMs have token limits. Full specs are too big to embed naively.

**Strategy**:
- Include only relevant `paths`, `schemas` (via `$ref`)
- Strip comments, descriptions
- Normalize YAML to AST-style JSON
- Inline-only if `x-photon-inline: true` is set
- Use `tokens = chars / 3.5` for budget estimation

**CLI Support**:
```toml
[ai.context]
token_budget = 12000
compress = true
include_examples = false
```

---

### 🔁 Streaming Responses

**Why**: Responses for full OpenAPI paths or models may be large. Blocking UX is poor.

**Strategy**:
- Use OpenAI-compatible streaming (`stream: true`)
- Display tokens incrementally:
  ```
  [AI STREAM] → chunk...
  [AI STREAM] → next...
  ```
- CLI flag: `--stream` or `photon.toml` default

**Integration**:
- CLI: streamed JSON assembled client-side
- SaaS: use event stream via WebSocket or SSE

---

### 🔏 Secure Prompt Logging (Opt-in + Redaction)

**Why**: Some field names or schemas may be sensitive (e.g., `password`, `token`, `email`)

**Strategy**:
- `.photonignore-fields` config
- Redact fields before serializing:
  ```json
  { "name": "string", "password": "<redacted>" }
  ```
- Logging is off by default, opt-in via:

```toml
[ai.logging]
enabled = true
log_path = "logs/prompts.jsonl"
redact = ["password", "token", "secret"]
```

**Output Format**: newline-delimited JSON

---

### 🔂 Prompt Replay & Versioning

**Why**: To reproduce AI-generated outputs or review previous suggestions

**Structure**:
```json
{
  "timestamp": "2024-06-01T12:34:00Z",
  "intent": "generate-model",
  "prompt": "Create a model for BlogPost...",
  "response_hash": "abc123",
  "tokens_used": 2345,
  "version": "v1"
}
```

- Replay via `photon ai --replay <hash>`
- Versioned templates for AI guidance

---

This system design ensures Photon AI is performant, observable, secure, and extensible for both local and SaaS workflows.
