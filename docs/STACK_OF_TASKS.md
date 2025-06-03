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

- [ ] Define AI prompt schema + response model
- [ ] Implement `photon ai suggest-path`
- [ ] Implement `photon ai generate model`
- [ ] CLI backend prompt-to-code pipeline
- [ ] Server-side prompt routing logic for SaaS

---

## ☁️ Phase 3 – SaaS Alpha

- [ ] Build SolidJS/Next.js frontend with schema editor
- [ ] API endpoints for project + spec CRUD
- [ ] GCP service account onboarding script
- [ ] Deploy preview infra using GCP Cloud Run or ephemeral containers
- [ ] Integrate GitHub export + deploy hooks

---

## 🔬 Phase 4 – Pact Contracts

- [ ] Auto-generate Pact consumer contracts from OpenAPI
- [ ] Implement Pact provider verifier harness
- [ ] Scaffold test suite templates from response examples

---

## 🧰 Infra / Ops / Support Tools

- [ ] Write Medium blog post: *Markdown-First AI — Supercharging ChatGPT for Developer Velocity*
- [ ] Draft `README.md` or `gist.md` for public release of Markdown-First AI concept
- [ ] Define `photon.toml` config schema
- [ ] GitHub Actions deploy template
- [ ] Bootstrap GCP project with Crossplane/Upbound

---

## 🛠️ photon-engine Template System (Phase 1.5 Planning)

- [ ] Scaffold `photon-engine` crate structure (lib.rs, context.rs, dispatcher.rs)
- [ ] Design file output strategy (dry-run, overwrite-safe)
- [ ] Build engine dispatcher (template mapping, conditional logic)
- [ ] Write `generate_model_files()` entry point using context API
- [ ] Define template registration mechanism for Askama
- [ ] Plan unit + integration testing strategy for file rendering

- [ ] Support user-supplied OpenAPI specs via `--openapi path/to/spec.yaml`
- [ ] Sanitize and normalize imported OpenAPI documents
- [ ] Guide user through interactive validation and correction to ensure:
    - OpenAPI version is 3.1+
    - Schema components are named, typed, and referenced correctly
    - Path objects contain valid operation objects and responses
    - Photon conventions are met (e.g., operationId, tag formatting, consistent naming)
- [ ] Emit a Photon-conformant `openapi.yaml` with a backup of the original
- [ ] Implement Photon OpenAPI rule engine
