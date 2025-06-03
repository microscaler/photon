# 📊 PHOTON_MICRO_LLM_SELECTION.md

## 🧠 Recommended Model for Photon Micro-LLM

### 🏆 Best Fit: **Mistral 7B**

| Feature                | Why It Matters                                          |
|------------------------|----------------------------------------------------------|
| 🧠 Strong Reasoning    | Handles OpenAPI path/schema comprehension and generation|
| ⚡ Quantized to ~4.4GB | Runs on most dev laptops with 8–16GB RAM                |
| 🧰 LoRA-compatible     | Easy to fine-tune with low-resource adapters            |
| 🌍 Ecosystem Support   | Runs on Ollama, llama.cpp, Hugging Face, TextGen UI     |

---

## 🧪 Comparison Overview

| Model        | Params | Ideal Use Case                                  | On-Disk Q4 Size |
|--------------|--------|--------------------------------------------------|-----------------|
| Mistral 7B   | 7B     | Default Photon micro-LLM target                   | ~4.4 GB         |
| Phi-2        | 2.7B   | Smaller memory, simpler prompt tasks             | ~1.8 GB         |
| TinyLLaMA    | 1.1B   | Quick inference, minimal resources                | ~0.6 GB         |
| Gemma 2B     | 2B     | Lightweight, clean tokenizer, minimal logic paths| ~1.2 GB         |

---

## 🎯 Selection Summary

- Use **Mistral 7B (Q4)** as the default base for fine-tuning.
- Pair with QLoRA adapters trained on OpenAPI prompt-response pairs.
- Deploy via **Ollama**, and expose over HTTP for CLI inference.

---

## 🧩 Sample Integration Config

```toml
[ai]
provider = "ollama"
model = "photon-openapi"
url = "http://localhost:11434"
```

---

## 🔄 Future Option: Serve via local Photon SaaS agent or gRPC microservice.
```bash
photon ai suggest-path "POST /register user"
```

Let me know if you'd like to tick this off in the stack as committed.
