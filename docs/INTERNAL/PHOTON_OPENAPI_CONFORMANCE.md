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
    - Have at least one valid HTTP method (`get`, `post`, etc.)
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
- Required for any templated path (`/users/{id}`)
- Must include:
    - `name`: matches path segment
    - `in`: `"path"`, `"query"`, or `"header"`
    - `schema.type`: valid OpenAPI primitive
- No unnamed or schemaless parameters

### ✅ RequestBodies
- Must use `$ref` to a schema in `components.schemas`
- Must define `application/json` content type

### ✅ Responses
- Must declare `description` and `content` per status code
- Must include a `200` or `201` response with a schema
- **All schemas in responses must include type bounds**:
    - `array`: `minItems`, `maxItems`
    - `object`: `minProperties`, `maxProperties`
    - `string`: `minLength`, `maxLength`
    - `number` / `integer`: `minimum`, `maximum`
    - `enum`: defined `enum` list
    - `date` / `date-time`: `format` present

### ✅ Tags
- Use PascalCase or kebab-case (`UserAuth`, `BlogPosts`)
- All paths must include at least one tag

### ✅ Authentication (Security)
- Must define at least one security scheme under `components.securitySchemes`
- Acceptable types:
    - `http` (basic or bearer)
    - `apiKey`
- All operations must:
    - Inherit security from root, or
    - Override with a specific `security` declaration

---

## 💡 Photon-Specific Conventions

- `operationId`: must be camelCase and globally unique
- Paths must follow model/resource structure: `/users`, `/users/{id}`
- Schema names = PascalCase matching model name
- Canonical CRUD `operationId` forms:
    - `getUsers`, `getUser`, `createUser`, `updateUser`, `deleteUser`
- Request body schema = input
- `200` response schema = output

---

## 🧪 Validation Strategy

- Implemented in:
    - `photon openapi navigate`
    - `photon dev`
- Uses `openapiv3` + Photon rule engine
- CLI presents:
    - Errors with path/line context
    - AI-assisted fix suggestions (if enabled)
- Validated before codegen, deploy, test generation


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

