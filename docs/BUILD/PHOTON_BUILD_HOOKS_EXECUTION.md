# 🧪 Photon Build Hook Execution Strategy

## 🧭 Purpose

Enable pre- and post-build custom logic to be executed in a portable, repeatable way across environments, projects, and deployment targets. Hook commands extend the Photon build lifecycle using user-defined shell or script instructions.

---

## 📁 Example `photon.toml` Configuration

```toml
[build.hooks]
pre = ["echo 'Starting build...'", "scripts/setup_env.sh"]
post = ["scripts/post_build_artifacts.sh", "echo 'Build finished.'"]
```

---

## ⚙️ Execution Model

- Hooks are executed in declaration order using `sh -c '<command>'`
- Phases:
    - `pre`: before any backend/frontend build
    - `post`: after backend and frontend build complete
- All commands execute in project root
- Non-zero exit status causes the build to abort (unless `--allow-fail-hooks` is passed)

---

## ✅ Available Environment Variables

| Variable        | Description                          |
|-----------------|--------------------------------------|
| `PHOTON_ENV`    | `"dev"` or `"build"`                 |
| `PHOTON_STAGE`  | `"pre"` or `"post"` (current hook)  |
| `PHOTON_OUTPUT` | Absolute path to `/dist/` directory  |

---

## 🧪 Logging & Dev Experience

- Logs:
    - `[HOOK][pre] running: scripts/setup_env.sh`
    - `[HOOK][post] completed: 1.4s`
- Captures and prints stdout/stderr per hook
- Clearly surfaces failing commands
- Exit code propagation to main `photon build` process

---

## ❗ Failure Handling

- Hook failure = build failure by default
- CLI flag `--allow-fail-hooks` allows continuation
- All failures are logged inline with the source command

---

## 🔮 Future Enhancements

- Hook profiling (time per command)
- Conditional hooks (e.g., `post:frontend`)
- External hook definition via `photon.hooks.json`
- Async parallel hook batching with dependencies

