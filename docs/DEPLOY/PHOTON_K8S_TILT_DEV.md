# 🔁 Photon Local Kubernetes Dev with Tilt + Kind

## 🧭 Purpose

Enable a rapid local feedback loop using:
- Tilt: for file sync, rebuild, logs, health checks
- Kind/k3s: for running the Photon app on local Kubernetes
- `photon dev --target tilt`: to bootstrap the flow from CLI

---

## 📝 Dev Experience

```bash
photon dev --target tilt
```

- Watches code and `openapi.yaml`
- Triggers rebuilds of backend and frontend
- Live syncs static UI files and rebuilt Rust binary
- Tilt UI (web) shows logs, health checks, service graphs

---

## 📁 Generated Files

```plaintext
tilt/
├── Tiltfile
├── k8s/
│   ├── api-deployment.yaml
│   ├── ui-deployment.yaml
│   └── shared-config.yaml
├── .tiltignore
└── .env
```

---

## 🧩 Tiltfile Includes

- `docker_build()` or `custom_build()` for Rust binary
- `k8s_yaml()` includes Deployment + Service
- `k8s_resource()` configures auto-reload, readiness probes
- Mounts `./ui/dist` and `target/release/myapp`

---

## ⚙️ Prerequisites

- Docker
- Tilt (`brew install tilt`)
- Kind or k3s
- Photon project with `openapi.yaml` and valid build

---

## 🔧 Photon CLI Integration

- `photon dev --target tilt`:
    - Ensures Tilt is installed
    - Writes Tiltfile and supporting manifests
    - Starts Tilt dashboard or CLI

---

Would you like to commit this as `docs/DEPLOY/PHOTON_K8S_TILT_DEV.md` and mark Tilt setup spec as complete in the stack?
