# 📍 Photon Project Roadmap

A milestone-based development plan for Photon’s CLI, runtime, and SaaS platform.

---

## ✅ Phase 0 – Planning & Architecture

- [x] Vision definition (`VISION.md`)
- [x] SaaS architecture + flows (`PLATFORM_VISION.md`, `ARCHITECTURE.md`)
- [x] Stack of next tasks
- [x] Sequence diagrams for core interactions

---

## 🚧 Phase 1 – CLI MLP

**Goal:** Enable full-stack project generation from OpenAPI-first spec.

### Features
- [ ] `photon new` - Project scaffold
- [ ] `photon generate model` - Generates Rust model + schema + UI
- [ ] `photon openapi navigate` - CLI for editing OpenAPI spec
- [ ] `photon ui generate form` - Generate SolidJS form from schema
- [ ] `photon build` - Compile backend + frontend bundle
- [ ] Basic test runner + formatter

---

## 🧠 Phase 2 – AI Integration

**Goal:** Boost developer velocity through natural language generation.

### Features
- [ ] `photon ai suggest-path "GET /posts"` → OpenAPI path + handler stub
- [ ] `photon ai generate model User name:String` → schema + struct
- [ ] CLI integration with LLM backend
- [ ] API endpoint for SaaS-based AI prompts

---

## ☁️ Phase 3 – SaaS Alpha

**Goal:** Deliver MVP web-based Photon experience with Git/GCP deploy.

### Features
- [ ] SolidJS/Next.js UI for OpenAPI editing
- [ ] Backend API to persist specs + files
- [ ] Deploy-to-GCP via delegated access
- [ ] Tenant infra with Crossplane in GKE namespace
- [ ] GitHub push/export functionality
- [ ] Live preview environment per project

---

## 🔬 Phase 4 – Contracts & Testing

**Goal:** Guarantee inter-service reliability and test safety via Pact.

### Features
- [ ] Pact consumer generator from OpenAPI
- [ ] Pact provider verifier wrapper
- [ ] Test stub generation from example responses

---

## 🌍 Phase 5 – Production Platform

**Goal:** Photon SaaS enters hosted service phase with CI/CD and team support.

### Features
- [ ] Multi-user team auth & RBAC
- [ ] Deployment logs + preview logs
- [ ] Plugin registry (middleware, auth, DB adaptors)
- [ ] Billing + project limits

---

## 🧰 Supporting Tools

- [ ] GitHub Actions template
- [ ] GCP org bootstrap script
- [ ] CLI self-update mechanism
