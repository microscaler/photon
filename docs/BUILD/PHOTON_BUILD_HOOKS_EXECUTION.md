# 🧪 Build Hook Execution Strategy (CLI)

## 🧭 Purpose

Run user-defined pre- and post-build hooks declared in `photon.toml` to extend and customize the build process with shell commands, scripts, or tools.

---

## 🔧 Hook Locations

Hooks are declared like this in `photon.toml`:

```toml
[build.hooks]
pre = ["echo 'Cleaning'", "scripts/setup_env.sh"]
post = ["scripts/post_build_artifacts.sh"]
```

---

## ⚙️ Execution Model

- Each command is executed with `sh -c <command>`
- Commands run **synchronously**, in declared order
- All paths are relative to project root
- Non-zero exit status **aborts build** unless `--allow-fail-hooks` is passed

---

## ✅ Environment Variables Available

| Variable        | Description                          |
|-----------------|--------------------------------------|
| `PHOTON_ENV`    | `"dev"` or `"build"`                 |
| `PHOTON_STAGE`  | `"pre"` or `"post"` (current hook)  |
| `PHOTON_OUTPUT` | Path to `/dist/` directory           |

---

## 🧪 Dev Experience

- Logs each hook before/after execution
- Captures stdout and stderr
- On failure: prints error, aborts build (by default)

---

Would you like to commit this as `docs/BUILD/PHOTON_BUILD_HOOKS_EXECUTION.md` and mark the corresponding stack item ✅?
