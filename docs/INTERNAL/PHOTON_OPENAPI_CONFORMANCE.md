# ✅ Photon OpenAPI Conformance Ruleset

## 🧭 Purpose

To ensure that all OpenAPI documents used in Photon-powered projects are consistent, valid, and automation-ready. This enables:

- Accurate code generation
- Predictable runtime dispatch (BRRTRouter)
- Clean UI scaffolding
- Safe integration with Pact, AI, and plugins

---

## 📐 Required Conformance Rules

### ✅ OpenAPI Version
- Must be **`3.1.0` or higher**
- Declared at root: `openapi: 3.1.0`

### ✅ Paths
- Every path must:
    - Have at least one valid HTTP method (get, post, etc.)
    - Define a unique `operationId`
    - Include a `summary` or `description`
    - Include at least one valid `response`

### ✅ Components/Schemas
- All schemas must:
    - Be named in `components.schemas`
    - Use `type`, not `nullable` as root (no type-free objects)
    - Declare `properties`, `required`, and `additionalProperties: false`
- No untyped properties or anonymous schema blocks

### ✅ Parameters
- Must declare `name`, `in`, and `schema.type`
- No mixed location ambiguity (`query`, `path`, `header`) 

### ✅ RequestBodies
- Must use `$ref` to a schema in `components.schemas`
- Must define `application/json` content type

### ✅ Responses
- Must declare `description` and `content` per status code
- Must include a `200` or `201` response with schema

### ✅ Tags
- Use PascalCase or kebab-case (`UserAuth`, `BlogPosts`)
- All paths must include at least one tag

---

## 💡 Photon-Specific Conventions

- `operationId` must be camelCase and unique across project
- Route paths must match model-based structure (`/users/{id}`)
- Schema names must match PascalCase `Model` names
- CRUD endpoints must follow canonical operations:
    - `getUsers`, `getUser`, `createUser`, `updateUser`, `deleteUser`
- Input schema = request body
- Output schema = `200` response

---

## 🧪 Validation Strategy

- Built into `photon openapi navigate` and `photon dev`
- Uses `openapiv3` parser + custom Photon rule engine
- Errors displayed in interactive CLI wizard
- Optionally backed by AI assist to fix

---

Would you like to commit this as `docs/INTERNAL/PHOTON_OPENAPI_CONFORMANCE.md` and link it into the engine validation workflow?


Questions or suggestions for additional rules?

### ✅ Parameters

Not having parameters defined correctly can lead to runtime errors and unexpected behavior, however how would we 
have a rich path without parameters?
    - `name`
    - `in` (query, path, header)
    - `schema.type`

### ✅ Authentication definitions
- Must define security schemes in `components.securitySchemes`
- Must reference security schemes in `security` at root or operation level

### ✅ Responses
Responses must be well-defined to ensure clients can handle them correctly.
Responses must have bounds on types:
 - int (`integer`), float (`number`), string, boolean, array, object
 - must have bounds on arrays (e.g., `minItems`, `maxItems`)
 - must have bounds on objects (e.g., `minProperties`, `maxProperties`)
 - must have bounds on strings (e.g., `minLength`, `maxLength`)
 - must have bounds on numbers (e.g., `minimum`, `maximum`)
 - must have bounds on integers (e.g., `minimum`, `maximum`)
 - must have bounds on booleans (e.g., `true`, `false`)
 - must have bounds on enums (e.g., `enum` values)
 - must have bounds on dates (e.g., `format: date`, `format: date-time`)
 - must have bounds on times (e.g., `format: time`, `format: duration`)
 - must have bounds on datetimes (e.g., `format: date-time`, `format: timestamp`)

This is necessary because one of the up comming features of BRROTRouter is to allow 
for runtime validation of requests before passing on to handler (or reject) and responses against the OpenAPI schema.

