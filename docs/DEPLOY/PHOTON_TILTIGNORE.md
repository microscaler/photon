# 📁 `.tiltignore` Design for Photon

## 🧭 Purpose

Prevent Tilt from watching, syncing, or rebuilding on changes to files or directories that are not relevant to live development.

---

## 📂 Recommended `.tiltignore`

```plaintext
# Build artifacts
/dist
/target
/node_modules

# IDE and editor noise
.vscode
.idea

# Git
.git
.gitignore

# OS-specific
.DS_Store
Thumbs.db

# Logs and generated output
logs
*.log
*.bak
.env*
```

---

## 🔧 Behavior in Tilt

- Tilt will ignore these paths during `sync()` and `live_update`
- Reduces unnecessary rebuilds and CPU usage
- Ensures `.env`, build outputs, and editor configs don’t cause restarts

---

## 🛠️ CLI Integration

- `photon dev --target tilt` will:
    - Auto-generate `.tiltignore` if not found
    - Merge with any project-specific exclusions

---

Would you like to commit this as `docs/DEPLOY/PHOTON_TILTIGNORE.md` and tick off the related stack item?
