# Inside photon.toml

[build.hooks]
pre = ["scripts/setup_env.sh", "echo 'Preparing build...'"]
post = ["echo 'Build complete'", "scripts/post_build_artifacts.sh"]
```

---

### 📦 Build Hook Spec

| Phase     | Description                                        |
|-----------|----------------------------------------------------|
| `pre`     | Runs before any build step. Ideal for env setup, schema sync, cleanup |
| `post`    | Runs after both frontend and backend build complete. Useful for notifications, artifacts, tagging |

---

### 🔧 CLI Behavior

- Hooks executed in declared order via shell (`sh -c`)
- All commands run in project root
- `--skip-hooks` disables both
- Fail-fast on any non-zero exit

---

### 🛠️ Edge Features

- `PHOTON_ENV` environment var available in hook scope
- Supports `.sh`, `.ts`, `.js`, or shell inline strings
- Hooks may mutate output dir, push tags, etc.

---

Would you like to commit this as `docs/BUILD/PHOTON_BUILD_HOOKS.md` and check it off the stack?
