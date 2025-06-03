# 🛠️ `photon build` — Full Stack Project Builder

## 🧭 Purpose

To produce a clean, deployable build artifact for both backend and frontend. This includes:

- Compiling the Rust API using `cargo build --release`
- Building the SolidJS frontend via `vite build`
- Validating OpenAPI and regenerating any necessary code before build

---

## 📝 Usage

```bash
photon build [--backend-only | --frontend-only] [--profile dev|release] [--out ./dist]
```

---

## 🔁 Build Flow

1. Validate and sanitize `openapi.yaml`
2. Run `photon-engine` to sync codegen
3. If backend:
    - Run `cargo build --release`
    - Copy resulting binary and `api/openapi.yaml` into output
4. If frontend:
    - Run `vite build`
    - Copy compiled assets into `dist/ui/`

---

## 📂 Output Directory

```plaintext
/dist/
├── api/
│   ├── myapp (binary)
│   └── openapi.yaml
├── ui/
│   ├── index.html
│   ├── assets/
│   └── manifest.json
└── photon.toml
```

---

## ⚙️ Config Integration

Uses values from `photon.toml`:

```toml
[build]
backend_profile = "release"
frontend_dist = "ui/dist"
```

---

## 📦 Extensibility Model

- Support for `build hooks` (pre/post build) via shell or script config
- Alternate build targets: Docker image, WASM, static only
- Output format switch: `--format zip | dir | docker`

---

## 🧪 Future Enhancements

- Build caching for engine output
- Build report (compile time, sizes, warnings)
- Build matrix runner for CI (multi-arch)

---

Shall we commit this spec as `docs/BUILD/PHOTON_BUILD_STRATEGY.md` and mark the corresponding stack item done?
