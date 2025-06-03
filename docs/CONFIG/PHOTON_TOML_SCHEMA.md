# photon.toml — Project Configuration for Photon CLI and Engine

[project]
name = "myapp"
type = "fullstack" # options: fullstack, backend-only, frontend-only

[paths]
backend = "api"
frontend = "ui"
openapi = "api/openapi.yaml"

[codegen]
enabled = true
frontend = true
backend = true
watch_openapi = true
output_mode = "write" # write | dry-run | diff | force

[deploy]
provider = "gcp" # gcp | fly | custom
github_repo = "microscaler/myapp"
auto_commit = true

[testing]
pact = true
unit = true
integration = true

[ai]
enabled = true
model = "gpt-4"
provider = "openai"
prompt_log = "logs/prompts.json"

[security]
auth = "bearer" # or apiKey, none
scopes = ["admin", "user"]
```

---

## 🧭 Purpose

- Acts as a single source of config truth for:
  - CLI commands
  - Engine behavior (codegen, validation, runtime)
  - SaaS service expectations
  - Local development/devtools
- Keeps the project portable and automation-friendly

---

## 🧩 Integration Points

- `photon dev` reads paths and watch config
- `photon build` uses deploy config
- `photon ai` uses model/provider config
- `photon generate` obeys `codegen.output_mode`
- SaaS dashboard could parse and sync with it

---

Add to `docs/CONFIG/PHOTON_TOML_SCHEMA.md` and track schema in `photon-engine` and CLI?
