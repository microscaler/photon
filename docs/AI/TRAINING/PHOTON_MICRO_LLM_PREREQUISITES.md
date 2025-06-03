# 🧰 PHOTON_MICRO_LLM_PREREQUISITES.md

## 🧠 Objective

Set up a local environment for fine-tuning or adapting small language models to OpenAPI + Photon CLI-specific prompts.

---

## 🖥️ Hardware Requirements

| Component       | Minimum       | Recommended        |
|-----------------|---------------|--------------------|
| GPU (NVIDIA)    | 8 GB VRAM     | 16+ GB VRAM (3090+)|
| RAM             | 16 GB         | 32+ GB             |
| Storage (SSD)   | 20 GB free    | 100+ GB for dataset/ckpts |

---

## 🔧 Software Stack

| Tool            | Purpose                     | Install Hint                     |
|-----------------|-----------------------------|----------------------------------|
| Python 3.10+    | Core training stack          | via pyenv or conda               |
| CUDA Toolkit    | GPU acceleration             | Match driver version             |
| Docker          | Model serving (e.g. Ollama)  | docker.com                       |
| Git + Make      | Versioned training pipelines | apt/brew preinstalled            |

---

## 📦 Conda Environment Setup

```yaml
# photon-llm-env.yaml
name: photon-llm
channels:
  - conda-forge
dependencies:
  - python=3.10
  - pip
  - cudatoolkit=11.8
  - pip:
      - transformers
      - peft
      - accelerate
      - bitsandbytes
      - datasets
      - trl
      - sentencepiece
```

To create:
```bash
conda env create -f photon-llm-env.yaml
conda activate photon-llm
```

---

## 🧪 Optional Inference Runtime (Ollama)

```bash
brew install ollama
ollama run mistral
```

Photon CLI can connect to this for offline inference:
```toml
[ai]
provider = "ollama"
model = "photon-openapi"
```

---

Ready to move on to dataset design?
