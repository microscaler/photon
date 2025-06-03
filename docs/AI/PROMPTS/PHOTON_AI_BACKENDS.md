# 🧠 PHOTON_AI_BACKENDS.md

## 📦 Rust Crates for AI Integration

### ✅ `reqwest` + `serde_json`
- General-purpose HTTP client
- Use for direct LLM API calls (e.g., OpenAI, local server)
- Pros: flexible, async, well-supported

### ✅ `openai` crate
- [Crate: openai](https://docs.rs/openai/)
- Simple typed API for Chat and Completion endpoints
- Works well for basic non-streamed interactions

### ✅ `async-openai`
- Full async support + streaming + chat structure
- Best for CLI with streaming token UX
- Recommended default for Photon

---

## 🌐 Transport: REST API to OpenAI or Compatible LLMs

Photon’s `photon ai` uses REST APIs:

```http
POST https://api.openai.com/v1/chat/completions
Authorization: Bearer <token>
Content-Type: application/json
```

Payload structure:
```json
{
  "model": "gpt-4",
  "messages": [
    { "role": "system", "content": "You are a Rust and OpenAPI assistant." },
    { "role": "user", "content": "Suggest a GET /posts route with example schema." }
  ],
  "stream": true
}
```

---

## 🤖 “Micro-LLM” Idea: Train a Domain Expert Model

### 🎯 Vision
Train a small/medium model (e.g., Mistral or LLaMA2) focused exclusively on:
- OpenAPI
- Photon CLI prompts
- Schema inference from natural language

### 💡 Benefits
- Offline local usage
- Fast inference (Ollama / Llama.cpp)
- Photon-native understanding of codegen and spec conventions

### 🛠️ Tools & Training Options
- Base: Mistral 7B, TinyLlama, Phi-2
- Fine-tuning: QLoRA or PEFT
- Hosting: Local Ollama endpoint or custom REST server
- Prompt format: Same as OpenAI-compatible models

### 🚦 CLI Integration

```toml
[ai]
provider = "ollama"
model = "photon-openapi:latest"
url = "http://localhost:11434"
```

Command-line usage:

```bash
photon ai suggest-path "POST /login with JWT response"
--model photon-openapi
--provider local
```

---

## 🧪 Fallback Strategy

- Start with OpenAI as default
- Detect failures and fallback to local model if configured
- CLI flag `--failover` or auto-detect

---

This backend strategy unlocks powerful, flexible AI integration while maintaining portability and precision for spec-first workflows.
