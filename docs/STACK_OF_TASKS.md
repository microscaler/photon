# 🗂️ Stack of Next Tasks (Organized by Roadmap Phase)

A prioritized and categorized backlog of tasks to drive Photon development across CLI, SaaS, and infrastructure components.

---

## 🚧 Phase 1 – CLI MLP

- [ ] Create `photon new` scaffold generator
- [ ] Build `photon generate model` command
- [ ] Design and prototype `photon openapi navigate`
- [ ] Implement `photon ui generate form` (OpenAPI → SolidJS)
- [ ] Add `photon build` command (backend + frontend)

---

## 🧠 Phase 2 – AI Integration

### 📦 Micro LLM Planning
- [ ] Design prompt templates for CLI/route/schema modes
- [x] Implement OpenAPI prompt generator to create instruction-tuning data from scraped specs ✅ `PHOTON_OPENAPI_PROMPT_GENERATOR.md` committed
- [ ] Write OpenAPI scraping strategy to extract real-world training examples
- [ ] Implement OpenAPI scraper to collect and normalize public specs
- [ ] Define LLM training roadmap for OpenAPI-focused model
- [x] Document local setup prerequisites (Docker, Python, CUDA, etc) ✅ `PHOTON_MICRO_LLM_PREREQUISITES.md` committed
- [ ] Evaluate local vs cloud (Hugging Face, Colab, AWS) training paths
- [x] Plan dataset structure: instruction-response pairs, OpenAPI schema coverage ✅ `Dataset-Design-for-the-Photon-micro-LLM.md` committed
- [x] Design validation/evaluation strategy (schema compliance, test harnesses) ✅ `PHOTON_MICRO_LLM_VALIDATION_STRATEGY.md` committed
- [x] Commit `PHOTON_MICRO_LLM_BOOTSTRAPPING.md` for GPT-based dataset generation ✅ committed
- [x] Commit `PHOTON_MICRO_LLM_SELECTION.md` with rationale for best model choice ✅ `Mistral 7B` selected
- [x] Commit `PHOTON_MICRO_LLM_TRAINING_PIPELINE.md` for fine-tuning a local model ✅ committed
- [x] Commit `PHOTON_MICRO_LLM_SIZING.md` with quantized model size breakdowns ✅ committed

### 🔌 AI Backend & Model Strategy
- [x] Finalize `PHOTON_AI_BACKENDS.md` for supported AI providers and CLI integration ✅ committed

### 🔐 Future AI Capabilities
- [x] Design token budgeting strategy for OpenAPI context embedding ✅ `PHOTON_AI_SYSTEM_DESIGN.md` committed
- [x] Support streaming AI responses in `photon ai` CLI ✅ `PHOTON_AI_SYSTEM_DESIGN.md` committed
- [x] Add secure prompt logging system with opt-in and redaction ✅ `PHOTON_AI_SYSTEM_DESIGN.md` committed
- [ ] Design prompt versioning and replay for reproducible AI output

- [x] Finalize AI prompt schema: input structure, context, and format ✅ `PHOTON_AI_PROMPT_SCHEMA.md` committed
- [ ] Define response model: OpenAPI, code snippets, CLI decisions
- [x] Add AI backend support to Photon CLI (`photon ai <prompt>`) ✅ `PHOTON_AI_COMMAND_EXECUTION.md` committed
- [ ] Define `ai` commands:
    - `suggest-path`
    - `generate-model`
    - `refactor-schema`
    - `doc-route`
- [ ] Plan SaaS server LLM integration:
    - Provider abstraction: OpenAI, Claude, local
    - Token limits, streaming, retry
- [ ] Define AI system messages and prompt templates
- [ ] Implement prompt history + audit trail (`logs/prompts.json`)
- [ ] Write fallback strategy for missing context or malformed response
