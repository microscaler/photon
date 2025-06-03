# 🔧 Photon CLI Command Inventory (Design-Focused)

---

## `photon new`

> Scaffold a new full-stack project (Rust + SolidJS)

- Sets up repo structure, OpenAPI base, Tailwind, and config
- Flags: `--backend-only`, `--frontend-only`, `--no-git`, `--template`

---

## `photon generate model <Name> <field:type>...`

> Create a data model with backend + OpenAPI + form UI

- Generates:
    - Rust struct
    - OpenAPI schema component
    - SolidJS form (optional)
- Flags: `--no-ui`, `--no-client`, `--orm`

---

## `photon openapi navigate`

> Interactive CLI explorer/editor for OpenAPI specs

- Browse paths, components, and patch the spec
- Add new routes, generate schemas
- Flags: `--add-path`, `--add-schema`, `--validate`, `--ai`

---

## `photon ui generate form <SchemaName>`

> Generates SolidJS form from OpenAPI schema

- Creates TSX form component + optional page
- Flags: `--page`, `--route`, `--style tailwind`

---

## `photon build`

> Build backend and frontend into deployable artifacts

- Runs:
    - `cargo build` in `api/`
    - `vite build` in `ui/`
- Outputs `dist/` folder
- Flags: `--backend-only`, `--frontend-only`, `--watch`, `--clean`
- packages artifacts for deployment
- Outputs:
    - `api/target/release/myapp`
    - `ui/dist/`
- creates docker image if `--docker` is specified

---

## `photon dev`

> Starts full-stack dev server

- Runs API in one process, Vite dev server in another
- Auto-reloads on OpenAPI/model changes
- Flags: `--backend`, `--frontend`, `--port`

---

## `photon test`

> Run all tests (Rust + TS + Pact)

- Discovers and runs:
    - `cargo test`
    - `vitest` or `jest`
    - Pact contract verifications
    - OpenAPI spec validation
    - test suites
      - unit tests
      - integration tests
      - playwright tests

---

## `photon pact generate-consumer <endpoint>`

> Generate a Pact consumer contract for a specific path

---

## `photon deploy`

> Deploy app via GitHub, Fly.io, or GCP, or local Docker Compose

- Reads config from `photon.toml`
- Flags: `--target`, `--dry-run`, `--git-push`, `--cloud`

---

## `photon ai <natural language>`

> AI prompt interface

- Routes to:
    - suggest-path
    - generate model
    - refactor route
    - doc a schema
- Flags: `--suggest`, `--model`, `--path`, `--doc`

---

Would you like this CLI spec committed as `docs/CLI/PHOTON_CLI_COMMANDS.md` and linked in the stack?
