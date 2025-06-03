# 🧠 Photon AI Command Execution Strategy

## 🧭 Purpose

Enable AI-driven code generation, schema mutation, and route suggestion via a unified CLI command interface.

---

## 🧰 CLI Command Overview

```bash
photon ai <intent> "<prompt>" [--context path/to/openapi.yaml] [--output file]
```

### Supported Subcommands
```bash
photon ai suggest-path "Create GET /posts"
photon ai generate-model "User with name and email"
photon ai doc-route "Document POST /login"
photon ai refactor-schema "Split Post into DraftPost and PublishedPost"
```

---

## 🔧 Execution Flow

1. CLI parses intent and natural prompt
2. Collects OpenAPI + schema context from:
    - `photon.toml`
    - `api/openapi.yaml`
    - recent model files
3. Applies token budgeting and compression
4. Sends prompt + context to AI backend
5. Streams or receives structured response
6. Validates response structure (intent-specific)
7. Outputs result to file, STDOUT, or patches spec

---

## 🌐 Integration Modes

- **CLI (local)**: `photon ai` connects to OpenAI or local model
- **SaaS**: Photon backend handles prompt, streaming, and updates
- **Editor Plugin (Future)**: Command-exec backend reused via IPC or LSP

---

## 🧪 Safety Features

- Confirm before overwriting files
- Optional dry-run: `--dry-run`
- Output can be diffed against previous content

---

Would you like this committed as `docs/AI/PHOTON_AI_COMMAND_EXECUTION.md` and marked in the stack?
