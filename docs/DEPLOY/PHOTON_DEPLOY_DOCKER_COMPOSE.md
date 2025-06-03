# 🐳 Docker Compose Deployment Strategy

## 🧭 Purpose

Enable local or production-like deployment using Docker Compose. This helps developers simulate runtime infrastructure with minimal setup.

---

## 📁 Expected Output

```plaintext
dist/
├── docker-compose.yaml
├── Dockerfile.api
├── Dockerfile.ui
├── api/        # Rust build output
└── ui/         # Static frontend output
```

---

## 📝 CLI Usage

```bash
photon build --target docker-compose
photon deploy --target docker-compose
```

---

## 🧩 `docker-compose.yaml` Generated

```yaml
version: "3.8"
services:
  api:
    build:
      context: ./api
      dockerfile: ../Dockerfile.api
    ports:
      - "3000:3000"
  ui:
    build:
      context: ./ui
      dockerfile: ../Dockerfile.ui
    ports:
      - "5173:80"
```

---

## 🔧 Dockerfiles

- `Dockerfile.api`: `FROM rust:alpine`, copies built binary, exposes 3000
- `Dockerfile.ui`: `nginx:alpine`, copies built UI, serves on 80

---

## 🔌 Optional Features

- Use `.env` file for secrets
- Mount `volumes:` for persistent state
- Support `docker compose --profile production`

---

Would you like to commit this as `docs/DEPLOY/PHOTON_DEPLOY_DOCKER_COMPOSE.md` and tick off the stack item?
