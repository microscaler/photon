# PLATFORM_VISION.md

## ✨ Purpose

The Photon SaaS platform transforms Photon from a CLI-based development tool into a visual, collaborative, zero-install PaaS for full-stack Rust and SolidJS applications. It empowers users to build backend APIs and frontend interfaces from the browser using an OpenAPI-first approach, AI tooling, and 1-click deployment.

---

## 🚀 Goals

1. **Lower barrier to entry** for Rust app development.
2. **Empower non-Rust users** to visually build APIs, models, and UIs.
3. **Bring AI-powered productivity** to every part of the stack.
4. **Create a deployable full-stack Rust app** with zero config.
5. **Operate tenant infrastructure on their GCP with minimal cost.**

---

## 🧱 Architecture Overview

### 🔹 Frontend (Web UI)
- Built in SolidStart or Next.js.
- Provides:
    - Project dashboard
    - Schema and UI builders
    - AI-assisted coding tools
    - Live preview
    - GitHub integration and deploy triggers

### 🔹 SaaS API Server
- Built with Axum or Express
- Handles:
    - Auth, project CRUD, AI prompt resolution
    - Tenant isolation and orchestration
    - Communicates with Photon Engine and infra layer

### 🔹 Photon Engine
- A worker that wraps `photon` CLI
- Accepts OpenAPI + UI config, returns full codegen
- Runs in GKE or on Cloud Run jobs

### 🔹 Infra Management Layer
- Photon controls all tenant infra via **Crossplane/Upbound**
- Operates from a **central GKE cluster**
- Each tenant's Crossplane is deployed into a namespace
- All infra declared in Git (`infra-org/project-name.git`)

---

## 🔁 Key Flow Sequences

### 📦 New Project
```plaintext
User      → UI        : Create project
UI        → API       : POST /projects
API       → GCP/DB    : Store project metadata
API       → Engine    : scaffold OpenAPI + backend + frontend
Engine    → Storage   : Save files (GCS)
API       → UI        : return project & files
```

### 🛠️ Add Route / Model
```plaintext
User      → UI        : Adds model/route
UI        → API       : PATCH /spec
API       → Engine    : regenerate code
Engine    → Storage   : overwrite source
API       → UI        : update preview
```

### 🚀 Deploy
```plaintext
User      → UI        : Clicks 'Deploy'
UI        → API       : POST /deploy
API       → Crossplane: Apply new GCP manifests
API       → GitHub    : Push repo/trigger build
API       → UI        : Return deploy status/logs
```

---

## ☁️ GCP Deployment Design

| Area               | Approach                                  |
|--------------------|-------------------------------------------|
| Compute            | Cloud Run, optionally GKE                 |
| File storage       | GCS                                       |
| Metadata store     | Firestore or Postgres (Cloud SQL)         |
| Build pipeline     | GitHub Actions or Cloud Build             |
| Infra management   | Crossplane in tenant namespace            |
| Tenant isolation   | Git + GCP IAM + Crossplane scopes         |

---

## 🔐 Tenant Infra Principles

- Each customer gets a dedicated Git repo for infra manifests.
- Photon applies infra changes from within its GKE cluster using Crossplane.
- Least privilege is enforced using per-org service accounts.
- Deployments and builds occur in tenant’s GCP project to minimize TCO.

---

## 🧱 Deliverables

- ✅ `PLATFORM_VISION.md`
- ✅ API design
- ✅ Sequence flows
- ⏳ Diagrams for infra layout and multi-tenant control
- ⏳ Sample GCP org-delegate script
- ⏳ Deployment automation pipeline specs
