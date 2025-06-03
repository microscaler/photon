# ✨ `photon new` Command Specification

## 🧭 Purpose

Bootstraps a complete Photon full-stack project, including:
- Backend (Rust + BRRTRouter + Lifeguard)
- Frontend (SolidJS + Tailwind)
- Shared OpenAPI spec
- Initial layout for codegen, testing, and deploy

---

## 📝 Usage

```bash
photon new <project-name> [--full | --backend-only | --frontend-only]
```

---

## 📁 Project Layout

```plaintext
<project-name>/
├── api/
│   ├── openapi.yaml            # OpenAPI 3.1 spec (bootstrapped)
│   ├── src/
│   │   ├── handlers/           # Rust route handlers
│   │   ├── models/             # Data models
│   │   └── main.rs             # Entrypoint w/ BRRTRouter
│   └── Cargo.toml
├── ui/
│   ├── components/             # SolidJS components
│   ├── pages/                  # Routes mapped to OpenAPI ops
│   ├── tailwind.config.js
│   └── vite.config.ts
├── pact/
│   ├── consumer/               # Pact consumer contracts
│   └── provider/               # Pact verifier setup
├── photon.toml                 # Photon config (models, routes, deploy)
├── README.md
└── .gitignore
```

---

## 🔧 Flags

| Flag            | Description                             |
|-----------------|-----------------------------------------|
| `--full`        | (default) Sets up backend + frontend    |
| `--backend-only`| Only creates the Rust + OpenAPI backend |
| `--frontend-only`| Only sets up SolidJS + client code     |
| `--no-git`      | Skip git init                           |
| `--template <url>`| Use a custom template repo            |

---

## 📦 Generated Files

### `photon.toml`
```toml
[project]
name = "myapp"
type = "fullstack"

[paths]
backend = "api"
frontend = "ui"
openapi = "api/openapi.yaml"
```

### `openapi.yaml`
```yaml
openapi: 3.1.0
info:
  title: MyApp API
  version: 0.1.0
paths: {}
components:
  schemas: {}
```

---

## 🧠 Smart Defaults

- Initializes with an empty OpenAPI 3.1.0 file
- Creates a default `healthcheck` route + handler
- Bootstraps Tailwind + SolidJS form pages
- Adds working Pact consumer/provider contract files

---

## 🧪 Dev Experience

Post-run guidance printed:
```plaintext
✅ Project created at ./myapp

Next steps:
  cd myapp
  photon generate model User name email
  photon openapi navigate
  photon dev
```

---

Shall we proceed to define what the template files and logic in `photon new` actually look like next (e.g. default `main.rs`, `vite.config.ts`)?
