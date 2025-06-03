# ⚙️ photon-engine Template System

## 🧭 Purpose

A reusable code generation engine used by Photon CLI and SaaS to scaffold backend, frontend, and schema files. It powers:

- `photon new`
- `photon generate model`
- `photon ui generate form`
- `photon build`

---

## 🧱 Core Tech

- 🧩 **Template Engine**: [`askama`](https://github.com/djc/askama)
- 📂 **Template Structure**: Organized by domain
- 🔐 **Sandboxed Execution** (via CLI/engine separation)

---

## 📁 Template Layout

```
templates/
├── backend/
│   ├── model.rs.askama
│   ├── handler.rs.askama
│   └── main.rs.askama
├── openapi/
│   └── schema.yaml.askama
├── frontend/
│   ├── form.tsx.askama
│   └── page.tsx.askama
├── pact/
│   └── consumer.rs.askama
├── common/
│   └── photon.toml.askama
```

---

## 📦 Inputs to Engine

```rust
pub struct TemplateContext {
    pub project_name: String,
    pub model_name: String,
    pub fields: Vec<Field>,
    pub path: Option<String>,
    pub route_method: Option<String>,
    pub openapi: Option<OpenApiDoc>,
    pub frontend: bool,
    pub backend: bool,
}
```

```rust
pub struct Field {
    pub name: String,
    pub type_: String,
    pub format: Option<String>,
    pub required: bool,
}
```

---

## ✨ Template Example – `model.rs.askama`

```rust
use serde::{Deserialize, Serialize};

#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct {{ model_name }} {
    {% for field in fields %}
    pub {{ field.name }}: {{ field.type_ }},
    {% endfor %}
}
```

---

## 🔁 Generation Flow

1. CLI gathers context from command
2. `photon-engine` receives `TemplateContext`
3. Askama templates are rendered
4. Files are written to appropriate directories

---

## 🧠 Smart Features

- Applies Rust field formatting rules (`snake_case`)
- Adds serde derives only if needed
- Supports conditionals (e.g., `#[derive(SeaOrm)]`)
- Maps field names → frontend widgets automatically

---

## 🧪 Dev Experience

When you run:

```bash
photon generate model User name:string age:int
```

You get:

- `api/src/models/user.rs`
- `api/openapi.yaml` component entry
- `ui/components/UserForm.tsx`

All generated from templated sources, with zero runtime logic in CLI.

---

## 🔄 Next Steps

- Set up `photon-engine` crate with Askama templating
- Define `TemplateContext` trait or impls
- Register templates and implement dispatcher
- Add CLI subcommands to test rendering

---

Shall we add this spec as `docs/INTERNAL/PHOTON_ENGINE_TEMPLATE.md` and start designing the context/dispatch structure in Rust?
