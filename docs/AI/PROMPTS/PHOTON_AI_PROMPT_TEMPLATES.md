# 🧠 PHOTON_AI_PROMPT_TEMPLATES.md

## 🧭 Objective

Define structured and consistent natural language prompt templates for all major AI-assisted tasks within Photon. These templates help align LLM output to expected OpenAPI, Rust, and CLI behavior.

---

## 📘 Template: `suggest-path`

```text
You are a Rust backend developer. Write an OpenAPI 3.1 path object for a {method} request to `{path}`.
The endpoint should {summary}. Use camelCase for operationId.
Respond only with the OpenAPI-compliant JSON fragment for this path.
```

---

## 📘 Template: `generate-model`

```text
Generate a Rust struct and OpenAPI component schema for a model named `{model_name}`.
The model has fields: {fields}. Use `snake_case` for Rust fields and `camelCase` for JSON.
Respond with:
- `rust_struct`
- `openapi_schema`
```

---

## 📘 Template: `doc-route`

```text
Write a summary and description for:
- Method: {method}
- Path: {path}
- Operation ID: {operationId}
Return in Markdown:
- Summary
- Description
```

---

## 📘 Template: `refactor-schema`

```text
Given this OpenAPI schema, suggest how to refactor it into smaller components.
Explain your decision. Output refactored schemas and their relationships.

Schema:
{schema}
```

---

## 📘 Template: `generate-test`

```text
Write a Rust integration test for `{method} {path}` using `reqwest`.
Use request data: {input}
Assert expected JSON fields in response.
```

---

## 📘 Template: `summarize-schema`

```text
Explain the following OpenAPI schema in plain English.
Describe fields, types, and usage.

{schema}
```

---

## 📘 Template: `migrate-schema`

```text
Compare two OpenAPI schemas and suggest a migration plan.
Highlight field renames, removals, and type changes.

From: {schema_v1}
To: {schema_v2}
```

---

## 📘 Template: `validate-openapi`

```text
Lint this OpenAPI path object. Identify:
- Missing fields
- Poor naming
- Unclear summaries
Return suggestions as a bullet list.

{operation_json}
```

---

## 📘 Template: `generate-impl-block`

```text
Generate a Rust `impl` block for controller `{function_name}`.
Accepts: `TypedHandlerRequest<{request_type}>`
Returns: `{response_type}`

Includes:
- Input validation
- DB call (SeaORM)
- Structured response

Respond with the Rust block only.
```

---

## 📘 Template: `generate-model-impl`

```text
Generate a Rust `impl` block for the SeaORM model `{model}`.
Include:
- create()
- find_by_id()
- update()
- delete()

Use `ActiveModel`, `EntityTrait`.
```

---

## 📘 Template: `generate-entity-from-ddl`

```text
Given the SQL DDL, generate:
- A Rust struct
- SeaORM Entity definition
- OpenAPI schema

DDL:
{sql_ddl}

Respond with:
- `rust_struct`
- `seaorm_entity`
- `openapi_schema`
```
