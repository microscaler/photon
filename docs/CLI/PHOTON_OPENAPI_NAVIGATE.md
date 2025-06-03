# 🧭 `photon openapi navigate` Command Specification

## 📌 Purpose

Interactive CLI tool to help developers view, edit, and extend their OpenAPI 3.1 spec directly from the terminal — with support for:
- Navigating existing paths, operations, and schemas
- Adding new routes with method, summary, and operationId
- Creating/editing component schemas
- Validating the spec
- AI-assisted generation (optional)

---

## 📝 Usage

```bash
photon openapi navigate
```

---

## 🧰 Features

### 🗺️ Path Navigation
- View a tree of existing paths and methods
- Select an endpoint to view/edit its metadata
- Add new paths with interactive prompts

### 📄 Schema Editor
- View defined components (schemas)
- Add new objects with properties, types, and required fields
- Modify properties via form-style prompts

### 🤖 AI Assist *(optional)*
```bash
> Describe the endpoint you want to add:
> "POST /login with email + password and returns a JWT"
```
→ Auto-generates full OpenAPI path item and schema components

### ✅ Validation
- Run `openapiv3` parser to check spec integrity
- Highlight missing fields, incompatible types, etc.

---

## 📁 Input/Output

- **Reads from:** `api/openapi.yaml`
- **Writes to:** `api/openapi.yaml` (in-place update)
- **Backups:** creates `openapi.backup.yaml` on each mutation

---

## 🧱 Interface Options

### CLI Menu (Default)

```plaintext
→ Paths
  └── /users
      ├── GET
      ├── POST
→ Components
  └── User
→ [A]dd Path
→ [S]chema Editor
→ [V]alidate Spec
→ [Q]uit
```

### Non-interactive Option

```bash
photon openapi navigate --add-path "/login POST"
photon openapi navigate --add-schema "Token jwt:string expires:datetime"
```

---

## 🧠 Smart Defaults

- Inserts new paths under correct tags
- Generates `operationId` from method + path
- Suggests responses based on status code conventions
- Suggests field types from names (e.g. `email` → `string + format: email`)

---

## 🧪 Dev Experience

After running:

```bash
photon openapi navigate
```

The developer can quickly:
- Add a new endpoint
- Define a schema inline
- Validate the updated spec
- Preview changes before committing

---

## 🔄 Next Steps

- Build TUI or CLI form-based editor (e.g. using `inquire`, `dialoguer`, or `crossterm`)
- Integrate with `openapiv3` crate
- Add AI bridge via local API or OpenAI call
- Write unit tests for YAML patching logic
