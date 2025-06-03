# 🛠️ PHOTON_MICRO_LLM_TRAINING_PIPELINE.md

## 🧭 Objective

Build and fine-tune a local LLM (e.g. Mistral 7B QLoRA) using the Photon OpenAPI dataset. The goal is to make the model respond like a Photon CLI co-pilot.

---

## 📁 Directory Structure

```plaintext
llm/
├── data/
│   └── photon-openapi.jsonl
├── models/
│   └── checkpoints/
├── scripts/
│   ├── train.sh
│   └── run_qlora.py
└── configs/
    └── qlora.yaml
```

---

## 🧪 Fine-Tuning Method: QLoRA

| Approach   | Notes                        |
|------------|------------------------------|
| Base       | Mistral 7B (HF or GGUF)      |
| Adapter    | PEFT / LoRA adapters         |
| Frameworks | 🤗 Transformers + `trl`, `peft`, `bitsandbytes` |
| Strategy   | 4-bit quant, ~20k prompt pairs, 2–4 epoch sweep |

---

## 📋 Example Config

```yaml
model_name_or_path: mistralai/Mistral-7B-v0.1
dataset_path: ./data/photon-openapi.jsonl
output_dir: ./models/checkpoints/
use_lora: true
load_in_4bit: true
lora_r: 8
lora_alpha: 16
lora_dropout: 0.1
per_device_train_batch_size: 4
gradient_accumulation_steps: 8
num_train_epochs: 3
save_strategy: "epoch"
```

---

## 🏁 Train Command

```bash
accelerate launch scripts/run_qlora.py \
  --config configs/qlora.yaml
```

---

## ✅ Result

After training:
- Export LoRA adapter
- Merge LoRA into full model (optional)
- Quantize to GGUF (for Ollama)
- Load with:
  ```bash
  ollama create photon-openapi --modelfile ./Modelfile
  ```

---

Want to mark this in the stack and commit as `PHOTON_MICRO_LLM_TRAINING_PIPELINE.md`?
