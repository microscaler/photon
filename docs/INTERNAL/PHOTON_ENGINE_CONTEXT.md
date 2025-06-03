# 🔧 photon-engine: Template Context & API

## 📦 Crate Name

```toml
[package]
name = "photon-engine"
version = "0.1.0"
edition = "2021"
```

---

## 📁 Module Structure

```plaintext
photon-engine/
├── src/
│   ├── lib.rs
│   ├── context.rs
│   ├── dispatcher.rs
│   └── templates/   # Askama templates
```

---

## 🧱 TemplateContext Definition

```rust
use serde::{Serialize, Deserialize};

#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct TemplateContext {
    pub project_name: String,
    pub model_name: Option<String>,
    pub fields: Vec<Field>,
    pub path: Option<String>,
    pub route_method: Option<String>,
    pub openapi: Option<String>, // YAML string
    pub frontend: bool,
    pub backend: bool,
}
```

### `Field`

```rust
#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct Field {
    pub name: String,
    pub type_: String,
    pub format: Option<String>,
    pub required: bool,
}
```

---

## 🔌 Engine API

### Function Interface

```rust
pub fn render_template(
    template_name: &str,
    context: &TemplateContext,
) -> Result<String, TemplateError>
```

### Dispatcher Example

```rust
pub fn generate_model_files(ctx: &TemplateContext) -> Result<HashMap<String, String>, TemplateError> {
    let mut files = HashMap::new();

    let model_code = render_template("backend/model.rs.askama", ctx)?;
    files.insert("api/src/models/".to_owned() + &ctx.model_name.as_ref().unwrap().to_lowercase() + ".rs", model_code);

    let openapi_snippet = render_template("openapi/schema.yaml.askama", ctx)?;
    files.insert("api/openapi.yaml.partial".into(), openapi_snippet);

    if ctx.frontend {
        let form_code = render_template("frontend/form.tsx.askama", ctx)?;
        files.insert("ui/components/".to_owned() + &ctx.model_name.as_ref().unwrap() + "Form.tsx", form_code);
    }

    Ok(files)
}
```

---

## 📤 Output Strategy

- Each call returns `HashMap<PathBuf, String>`
- CLI responsible for writing to disk, applying overwrite rules
- Can support dry-run mode or diff output

---

## 📋 Next Steps

- Scaffold crate
- Add Askama templates and register in `build.rs`
- Implement core dispatcher for model + form generation
- Add integration tests for common contexts
