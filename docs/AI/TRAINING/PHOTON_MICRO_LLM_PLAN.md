# 🤖 Training a Photon Micro-LLM for OpenAPI & CLI Codegen

## 🧭 Objective

Create a small, efficient model (≤7B params) trained specifically to:
- Suggest OpenAPI routes from prompts
- Generate request/response schemas
- Draft Rust handler stubs
- Propose model definitions

---

## 🧱 Model Selection

| Model        | Params | Notes                     |
|--------------|--------|---------------------------|
| Mistral      | 7B     | Fast, performant, supports quantization |
| TinyLLaMA    | 1.1B   | Lightweight, quick inferencing |
| Phi-2        | 2.7B   | Efficient for small memory |
| Gemma (2B)   | 2B     | Google-supported, good tokenizer |

Choose based on:
- Runtime (Ollama or llama.cpp)
- Target memory (<= 8GB RAM ideal)

---

## 📚 Training Data Plan

### Sources
- Public OpenAPI specs (curated)
- Photon route and model prompts + completions
- Canonical CRUD operations
- Prompt → OpenAPI examples
- `photon ai` command use cases

### Format

```jsonl
{"instruction": "Create GET /users", "response": "<OpenAPI JSON>"}
{"instruction": "Model for User with name and email", "response": "<Rust struct + OpenAPI schema>"}
```

---

## 🧠 Fine-Tuning Strategy

- Use LoRA or QLoRA (low-rank adapters) to fine-tune without full retrain
- Base model: Mistral or Phi-2
- Trainer: `Axolotl`, `Hugging Face PEFT`, or `OpenLLM`

```bash
# LoRA training launch example
accelerate launch train.py --config configs/photon.json
```

---

## 🧪 Evaluation Metrics

- Match OpenAPI schema format
- Valid JSON/YAML rate
- Semantic intent-to-output accuracy (e.g., “GET /users” → full path spec)
- Token efficiency for model size vs. fidelity

---

## 🚀 Hosting Options

- **Local**: Ollama (`ollama run photon-openapi`)
- **API**: expose model via REST with `text-generation-webui` or `lit-gpt`
- **Photon CLI**:
  ```toml
  [ai]
  provider = "ollama"
  model = "photon-openapi"
  ```

---

## 🔐 Distribution Model

- Bundle `.gguf` files for offline use
- Photon CLI downloads model on first use (`photon ai install-model`)

---

Would you like to commit this as `docs/AI/TRAINING/PHOTON_MICRO_LLM_PLAN.md` and add to the stack under Phase 2?
