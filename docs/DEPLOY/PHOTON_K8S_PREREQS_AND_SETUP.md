# 🧰 Prerequisites and Local Kubernetes Setup for Photon + Tilt

## 🧭 Goal

To enable seamless local development of full-stack Photon apps using:
- Docker (container runtime)
- Kind or k3s (lightweight Kubernetes)
- Tilt (live reload and orchestration)

---

## 📦 Required Tools

| Tool       | Description                             | Install Command                           |
|------------|-----------------------------------------|-------------------------------------------|
| Docker     | Container runtime for builds            | [Install Docker](https://docs.docker.com/get-docker/) |
| Tilt       | Kubernetes live reload orchestrator     | `brew install tilt` or [tilt.dev](https://docs.tilt.dev/install.html) |
| Kind       | Local Kubernetes using Docker           | `brew install kind` or `go install ...`   |
| k3s        | Lightweight Kubernetes alternative      | `curl -sfL https://get.k3s.io | sh -`     |
| kubectl    | Kubernetes CLI                          | `brew install kubectl`                    |

---

## 🗂️ Folder Structure

```plaintext
tilt/
├── Tiltfile
├── k8s/
│   ├── api-deployment.yaml
│   ├── ui-deployment.yaml
│   └── config.yaml
├── .tiltignore
└── .env
```

---

## 📝 Setup Flow

1. **Install required tools** (see table above)
2. **Create Kind cluster**:
   ```bash
   kind create cluster --name photon-local
   ```
3. **Start Tilt**:
   ```bash
   tilt up
   ```
4. Access Photon API at `localhost:3000`  
   Access Photon UI at `localhost:5173`

---

## 🌐 Notes

- Use `docker context` to ensure Docker targets Kind
- Prefer `k3s` if you want systemd-free environments or low footprint
- Consider using `ngrok` or `kubefwd` for external routing

---

Would you like to commit this as `docs/DEPLOY/PHOTON_K8S_PREREQS_AND_SETUP.md`?
