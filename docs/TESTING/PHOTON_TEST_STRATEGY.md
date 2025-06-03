# 🧪 `photon test` — Unified Test Strategy for Photon

## 🧭 Purpose

To provide a single CLI command to run all relevant tests for a Photon project:
- Rust backend unit/integration tests
- Pact provider contract verification
- Frontend (SolidJS) unit and component tests
- Snapshot/assertion diff testing

---

## 📝 Usage

```bash
photon test [--scope backend|frontend|pact|all] [--tag <filter>] [--watch]
```

### Examples

```bash
photon test --scope pact
photon test --scope all --tag critical
```

---

## 🎛️ CLI Options

| Flag        | Description                              |
|-------------|------------------------------------------|
| `--scope`   | Limit to `backend`, `frontend`, `pact`   |
| `--tag`     | Run only tests with matching tag metadata|
| `--watch`   | Watch mode (frontend/dev only)           |
| `--ci`      | Output test results in CI format (JUnit) |

---

## 🧩 What it Runs

| Test Type   | Tool         | Default Path               |
|-------------|--------------|----------------------------|
| Backend     | `cargo test` | `api/tests/`               |
| Pact        | Pact CLI     | `pact/consumer/*.json`     |
| Frontend    | `vitest`     | `ui/tests/` or `*.test.tsx`|
| Snapshot    | `insta` (TBD)| `tests/snapshots/`         |

---

## 📦 Output Formats

- Plain terminal output
- `--ci` writes:
    - `junit.xml`
    - `results.json`

---

## 🧠 Smart Features

- Auto-discovers test files via `photon.toml`
- Supports skipping tagged tests (`#[ignore]`, `test.skip`)
- Pacts are verified only against matching provider base URL

---

## 🧪 Internals

- Uses `Command::new()` runner for subprocesses
- Consolidates results and exit codes
- Logs test status per section and total result

---

Shall I add this to the stack as finalized, and link the Markdown in `docs/TESTING/PHOTON_TEST_STRATEGY.md`?
