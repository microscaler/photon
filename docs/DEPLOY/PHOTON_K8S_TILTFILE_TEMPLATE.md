# 🧱 Tiltfile Template for Photon Projects

## 🧭 Purpose

Automate rebuilds, syncs, live reloads, and health monitoring of Photon API and UI inside a local Kubernetes cluster (Kind/k3s) using Tilt.

---

## 📝 Default Tiltfile Template

```python
docker_build("photon-api", "./api", live_update=[
    sync("./api/src", "/app/src"),
    run("cargo build --release"),
])

docker_build("photon-ui", "./ui", live_update=[
    sync("./ui", "/usr/share/nginx/html"),
    run("npm run build")
])

k8s_yaml([
    "tilt/k8s/api-deployment.yaml",
    "tilt/k8s/ui-deployment.yaml"
])

k8s_resource("photon-api", port_forwards=3000)
k8s_resource("photon-ui", port_forwards=5173)

config.define_string("env", "dev", "dev | build")
```

---

## 📁 File Structure

```plaintext
tilt/
├── Tiltfile
├── k8s/
│   ├── api-deployment.yaml
│   ├── ui-deployment.yaml
│   └── configmap.yaml
├── .tiltignore
└── .env
```

---

## 🧠 Features

- Live reload on file change
- Inline logs for both containers
- Port-forwarding for local access
- Mounts `api/` and `ui/` into Kind pods
- Profiles for `dev` and `build`

---

## 🔄 CLI Integration

```bash
photon dev --target tilt
```

- Checks for Tilt, Docker, Kind
- Writes default Tiltfile if missing
- Starts Tilt in dashboard or terminal mode

---

Would you like to commit this as `docs/DEPLOY/PHOTON_K8S_TILTFILE_TEMPLATE.md` and tick it off the stack?
