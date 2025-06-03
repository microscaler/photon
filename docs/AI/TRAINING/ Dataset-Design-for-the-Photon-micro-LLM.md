# 📁 PHOTON_MICRO_LLM_DATASET_STRUCTURE.md

## 🧠 Objective

Create a dataset that trains the model to:
- Interpret natural language prompts
- Generate OpenAPI path operations, schemas, and Rust models
- Match Photon CLI behavior (e.g., `photon ai suggest-path`)

---

## 📦 Dataset Format: Instruction-Tuning JSONL

Each line in the dataset is a structured prompt/response pair:

```json
{
  "instruction": "Create a GET /users endpoint that returns a list of user objects with id and email.",
  "input": "",
  "output": {
    "operation": {
      "path": "/users",
      "method": "get",
      "operationId": "getUsers",
      "summary": "List users",
      "responses": {
        "200": {
          "description": "Successful response",
          "content": {
            "application/json": {
              "schema": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "id": { "type": "string", "format": "uuid" },
                    "email": { "type": "string", "format": "email" }
                  },
                  "required": ["id", "email"]
                }
              }
            }
          }
        }
      }
    }
  }
}
```

---

## 🔀 Prompt Types

| Category        | Examples                           |
|----------------|------------------------------------|
| Route Gen      | "Create POST /login with JWT"      |
| Model Gen      | "User with name, email, password"  |
| Doc Gen        | "Describe GET /posts/:id"          |
| Refactor       | "Split Post into Draft + Published"|
| Explain        | "Explain this schema..."            |

---

## 🔧 Preprocessing Pipeline

- Deduplicate examples by `instruction` hash
- Strip unused OpenAPI fields (`description`, `deprecated`)
- Convert YAML → JSON for training
- Apply redaction for fields like `password`, `secret` if needed

---

## 📈 Dataset Stats (Goal)

- 10k to 50k high-quality examples
- Balanced across categories
- 80% train / 10% val / 10% test

---

Would you like to commit this and mark the stack item done?
