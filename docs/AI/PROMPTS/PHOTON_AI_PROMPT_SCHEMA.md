# 🧠 PHOTON_AI_PROMPT_SCHEMA.md

## 🧭 Purpose

Provide a structured, deterministic format for invoking AI-assisted tasks from Photon CLI or SaaS. Ensures clarity, traceability, and correctness of AI-generated code/specs.

---

## 📥 Prompt Input Schema

```json
{
  "prompt": "Describe a GET /users route that returns a list of users.",
  "intent": "suggest-path",
  "context": {
    "project": "myapp",
    "operationIds": ["getUsers"],
    "openapi": "<YAML string or parsed object>",
    "models": ["User", "Post"]
  }
}
```

### 🔍 Input Fields

| Field      | Type      | Description                              |
|------------|-----------|------------------------------------------|
| `prompt`   | string    | Natural language input                   |
| `intent`   | string    | One of: `suggest-path`, `generate-model`, `refactor-schema`, `doc-route` |
| `context`  | object    | Project + model context for accurate codegen |

---

## 📤 Expected Response Model (Generic)

Depending on `intent`, response may return:

- `operation` (for `suggest-path`)
- `schema` (for `generate-model`)
- `doc` (for `doc-route`)
- `patch` (for `refactor-schema`)

Example (suggest-path):

```json
{
  "operation": {
    "path": "/users",
    "method": "get",
    "operationId": "getUsers",
    "summary": "List all users",
    "responses": {
      "200": {
        "description": "List of users",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/User"
            }
          }
        }
      }
    }
  }
}
```

---

## 📘 Prompt Examples by Intent

### ✨ Basic GET with schema reference

```json
{
  "prompt": "GET /posts returns a list of posts.",
  "intent": "suggest-path"
}
```

### ✨ POST with structured request and custom response

```json
{
  "prompt": "POST /posts accepts title, content (markdown), and tags. Responds with id, slug, and created_at.",
  "intent": "suggest-path"
}
```

Expected Output:

```json
{
  "operation": {
    "path": "/posts",
    "method": "post",
    "operationId": "createPost",
    "summary": "Create a new blog post",
    "requestBody": {
      "required": true,
      "content": {
        "application/json": {
          "schema": {
            "type": "object",
            "properties": {
              "title": { "type": "string" },
              "content": { "type": "string", "format": "markdown" },
              "tags": {
                "type": "array",
                "items": { "type": "string" }
              }
            },
            "required": ["title", "content"]
          }
        }
      }
    },
    "responses": {
      "201": {
        "description": "Post created",
        "content": {
          "application/json": {
            "schema": {
              "type": "object",
              "properties": {
                "id": { "type": "string", "format": "uuid" },
                "slug": { "type": "string" },
                "created_at": { "type": "string", "format": "date-time" }
              },
              "required": ["id", "slug", "created_at"]
            }
          }
        }
      }
    }
  }
}
```

---

## 🧠 CLI Behavior

- Photon CLI builds context from OpenAPI and project models
- Passes prompt payload to local engine or LLM API
- Output is parsed and validated before file generation

---

## 🔐 Future Considerations

- Token size budgeting for embedded OpenAPI context
- Streaming responses (for large model payloads)
- Secure prompt logging (opt-in, redacted where needed)

