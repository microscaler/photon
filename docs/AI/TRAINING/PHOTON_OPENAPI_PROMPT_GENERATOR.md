# 🧠 PHOTON_OPENAPI_PROMPT_GENERATOR.md

## 🧭 Objective

Generate instruction-tuning data automatically from real OpenAPI specs. The goal is to reverse-engineer natural language descriptions from structured path objects and schemas.

---

## 🧩 Input

Single `PathItem` or `Operation` from parsed OpenAPI spec, e.g.:

```json
{
  "path": "/users",
  "method": "get",
  "operationId": "getUsers",
  "summary": "Get a list of users",
  "responses": { ... }
}
```

---

## 📘 Prompt Generation Modes

| Mode         | Description                                     |
|--------------|-------------------------------------------------|
| route        | “Describe the behavior of this route”           |
| model        | “Describe this schema as a natural prompt”      |
| doc          | “Write a CLI-level docstring for this operation”|
| refactor     | “Suggest how to split/combine these models”     |

---

## 🧪 Output Format

```json
{
  "instruction": "Create a GET /users endpoint that returns a list of users.",
  "input": "",
  "output": {
    "path": "/users",
    "method": "get",
    "operationId": "getUsers",
    "responses": { ... }
  }
}
```

---

## 🛠️ Generator Behavior

- Simplify OpenAPI fields
- Infer missing `summary` using GPT if needed
- Redact or replace sensitive fields
- Randomize format slightly to prevent model overfitting

---

## 🚀 CLI (Planned)

```bash
photon dataset prompts --from scraped/ --out prompts/
```

Flags:
- `--types route,model`
- `--refine-with gpt-4`
- `--min-fields 2`

---

Would you like this saved and committed as `PHOTON_OPENAPI_PROMPT_GENERATOR.md`?
