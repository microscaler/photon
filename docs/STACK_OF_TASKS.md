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

- [ ] Define `photon.toml` config schema
- [ ] GitHub Actions deploy template
- [ ] Bootstrap GCP project with Crossplane/Upbound
