# 🧰 Prerequisites and Local Kubernetes Setup for Photon + Tilt

## 🧭 Goal

To enable seamless local development of full-stack Photon apps using:
- Docker (container runtime)
- Kind or k3s (lightweight Kubernetes)
- Tilt (live reload and orchestration)

---

## 📦 Required Tools
| Tool       | Description                             | macOS Install Command                     | Linux (Debian) Install Command            | Windows (Chocolatey) Install Command      |
|------------|-----------------------------------------|-------------------------------------------|-------------------------------------------|-------------------------------------------|
| Docker     | Container runtime for builds            | [Install Docker](https://docs.docker.com/get-docker/) | `sudo apt-get install docker-ce`          | `choco install docker`                    |
| Tilt       | Kubernetes live reload orchestrator     | `brew install tilt` or [tilt.dev](https://docs.tilt.dev/install.html) | `curl -fsSL https://github.com/tilt-dev/tilt/releases/latest/download/tilt-linux-amd64 -o /usr/local/bin/tilt && chmod +x /usr/local/bin/tilt` | `choco install tilt`                      |
| Kind       | Local Kubernetes using Docker           | `brew install kind` or `go install ...`   | `curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64 && chmod +x ./kind && mv ./kind /usr/local/bin/kind` | `choco install kind`                      |
| k3s        | Lightweight Kubernetes alternative      | `curl -sfL https://get.k3s.io | sh -`     | `curl -sfL https://get.k3s.io | sh -`     | Not available                             |
| kubectl    | Kubernetes CLI                          | `brew install kubectl`                    | `sudo apt-get install kubectl`            | `choco install kubernetes-cli`            |
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
