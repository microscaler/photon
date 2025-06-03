# Photon: Vision Statement

## ✨ What is Photon?

**Photon** is a full-stack Rust framework and platform that empowers developers to build modern, high-performance applications at the speed of light. Combining OpenAPI-first development, coroutine-powered concurrency, AI-assisted scaffolding, and full-stack code generation (backend + frontend), Photon delivers a Rails-like experience for Rust developers who value control, speed, and safety.

Photon can be used via a CLI for local development or through a SaaS platform that brings visual tooling, AI guidance, and one-click deployment into the browser.

---

## 🔑 Core Principles

1. **OpenAPI as the Source of Truth**
    - All routes, models, requests, and responses are defined via OpenAPI.
    - Code is generated from contracts, not the reverse.

2. **CLI-Centric Developer Experience**
    - Scaffold entire projects, models, routes, UIs, and contracts with a single CLI.
    - Smart defaults, low boilerplate, zero config where possible.

3. **Full-Stack by Default**
    - Generate both backend (Rust) and frontend (SolidJS + TailwindCSS) from a unified spec.
    - Forms, pages, and client logic scaffolded from OpenAPI components.

4. **Contracts + Concurrency**
    - Pact-based contract testing is built in.
    - `may` crate provides coroutine-powered, blocking-style async I/O.

5. **AI-Enhanced Productivity**
    - Natural language prompts help scaffold endpoints, models, and schemas.
    - OpenAPI navigation, UI suggestions, and refactoring powered by LLMs.

6. **Visual Simplicity with SolidJS**
    - UI is generated from schema, with future WYSIWYG support.
    - Photon avoids Lepton's routing; BRRTRouter is the single source of truth for dispatch.

7. **Platform as a Delivery Mechanism**
    - Photon is not just a tool — it's a hosted builder, runtime, and deploy engine.

---

## 🎯 Minimum Lovable Product (MLP)

### 🚀 CLI Features

- `photon new <app>`: Full-stack project scaffolding
- `photon generate model <Name> <fields>`: Rust + schema + UI
- `photon openapi navigate`: CLI wizard for editing OpenAPI spec
- `photon ai suggest-path "GET /posts"`: AI-generated path, schema, handler
- `photon pact generate-consumer`: Pact test scaffold
- `photon ui generate form <Model>`: Generate SolidJS form from OpenAPI schema

### 🧠 AI Integration

- Generate new OpenAPI paths and models from natural language
- Suggest improvements, refactor operations, rename models
- Inline command-line and web interface prompts

### 🧰 Backend

- **BRRTRouter**: Coroutine-native, OpenAPI-dispatched routing
- **Lifeguard**: Safe, coroutine-based PostgreSQL pooling
- **SeaORM** (optional): ORM integration

### 🎨 Frontend

- **SolidJS**: Reactive UI framework
- **TailwindCSS**: Utility-first CSS framework
- **Form Generator**: Creates forms from OpenAPI request schemas
- **Client Generator**: TypeScript clients from OpenAPI

---

## 🧪 Contract Testing

Photon integrates Pact to enable consumer-driven development:
- Generate Pact consumers and provider verifiers
- Derive Pact tests from OpenAPI examples automatically
- CLI Support: `photon pact generate-consumer`, `photon pact verify-provider`

---

## 🖼️ UI Designer Vision (Stretch Goal)

A future **WYSIWYG UI Designer** lets users:
- Visually navigate schemas
- Drag/drop form elements
- Generate SolidJS components with validation and data binding
- Preview UI bound to live schema examples

If WYSIWYG is not feasible early, Photon will focus on generating SolidJS + Tailwind components directly.

---

## 🧭 SaaS Vision: Photon Platform

### 🌌 Goals

- Web-based builder for API + UI
- AI-guided schema and codegen
- Hosted preview + export to GitHub
- 1-click deploy (Fly.io, Railway, Shuttle)
- Authentication, secret management, CI/CD

### 🚦 Delivery Modes

1. **Online Codegen (MLP SaaS)**
    - Web UI to define OpenAPI + schema + UI
    - Backend runs CLI to generate full project
    - Download as ZIP or push to GitHub

2. **Visual App Builder**
    - TUI or Web UI to design APIs + pages
    - Real-time preview (SolidJS)
    - Project persistence + auth + editor UX

3. **Full PaaS**
    - Run backend + db + frontend
    - GitOps, staging/prod environments
    - Team collaboration, plugin marketplace

### 🧱 Platform Architecture

```plaintext
[Browser UI] --> [Photon SaaS API]
                     |
                     |--> OpenAPI Builder
                     |--> AI Assist
                     |--> Codegen Engine
                     |--> GitHub Export
                     |--> Deployment Hooks
```

---

## 🎨 CSS Strategy

- **TailwindCSS** as default (scaffolded via `photon ui init --css tailwind`)
- SolidJS + Tailwind integration out-of-the-box
- Future support: UnoCSS, Vanilla Extract

---

## 📁 Suggested Repo Layout

```
/photon
├── cli/              # Rust CLI core
├── runtime/          # Photon backend core
├── templates/        # Codegen templates
├── web/              # SaaS frontend (Solid/Next.js)
├── saas-api/         # Platform backend (API, LLM calls)
├── openapi/          # Common types & schema helpers
├── pact/             # Pact helpers
├── docs/
│   ├── VISION.md
│   ├── ROADMAP.md
│   ├── ARCHITECTURE.md
│   └── PLATFORM_VISION.md
```

---

## ✅ Next Steps

- Finalize CLI feature set
- Build codegen templates for backend and SolidJS frontend
- Implement AI-assisted CLI prompts + server integration
- Scaffold minimal SaaS web interface with OpenAPI + UI editor
- Define MVP hosting/deploy strategy
- Create VISION.md, ROADMAP.md, PLATFORM_VISION.md in repo
