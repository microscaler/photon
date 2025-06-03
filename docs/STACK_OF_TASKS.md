# 🗂️ Stack of Next Tasks (Organized by Roadmap Phase)

A prioritized and categorized backlog of tasks to drive Photon development across CLI, SaaS, and infrastructure components.

---

## 🚧 Phase 1 – CLI MLP

- [ ] Create `photon new` scaffold generator
- [ ] Build `photon generate model` command
- [ ] Design and prototype `photon openapi navigate`
- [ ] Implement `photon ui generate form` (OpenAPI → SolidJS)
- [ ] Add `photon build` command (backend + frontend)

---

## 🧠 Phase 2 – AI Integration

- [ ] Define AI prompt schema + response model
- [ ] Implement `photon ai suggest-path`
- [ ] Implement `photon ai generate model`
- [ ] CLI backend prompt-to-code pipeline
- [ ] Server-side prompt routing logic for SaaS

---

## ☁️ Phase 3 – SaaS Alpha

- [ ] Build SolidJS/Next.js frontend with schema editor
- [ ] API endpoints for project + spec CRUD
- [ ] GCP service account onboarding script
- [ ] Deploy preview infra using GCP Cloud Run or ephemeral containers
- [ ] Integrate GitHub export + deploy hooks

---

## 🔬 Phase 4 – Pact Contracts

- [ ] Finalize `PHOTON_PACT_STRATEGY.md` high-level integration
- [ ] Specify CLI behavior for `generate-consumer` and `verify-provider`
- [ ] Auto-generate Pact consumer contracts from OpenAPI
- [ ] Implement Pact provider verifier harness
- [ ] Scaffold test suite templates from response examples
- [ ] Define implementation plan for Pact support (build, verify, CI integration)
- [ ] Finalize `PHOTON_PACT_TEST_SCAFFOLD.md` and spec input/output behavior

---

## 🛠️ photon-engine Template System (Phase 1.5 Planning)

- [x] Define high-level implementation plan for photon-engine crate (entrypoints, output, error handling)

### 🔨 Build Logic Extensions

- [x] Define how `build hooks` (pre/post) are declared in `photon.toml`
- [x] Implement build hook execution strategy in CLI ✅ `PHOTON_BUILD_HOOKS_EXECUTION.md` finalized
- [ ] Support build output formats: `--format zip`, `--format dir`, `--format docker`
- [ ] Add support for alternate build targets:
    - Docker image
    - WASM builds
    - Static frontend bundle only

### 🚀 Build Infrastructure Strategy

- [ ] Determine default build strategy for local CLI
- [ ] Design GitHub Actions workflow template for Photon projects
- [ ] Define CloudBuild configuration for SaaS deploys

### 🧩 Post-Build Integration Design

- [ ] Plan artifact publishing (e.g., GitHub Releases, OCI containers)
- [ ] Add notification hooks (Slack, Email, Webhook)
- [ ] Explore IDE integration (e.g., VS Code status bar, tasks, LSP events)

### 📈 Future Build Enhancements

- [ ] Plan build output caching strategy (hash-based)
- [ ] Add build reports (duration, size, diff summary)
- [ ] Support matrix builds for multi-arch via CI

---

## 🎯 Deployment Target Support

### Kubernetes Deployment Targets

#### Local Dev (Kind/k3s + Tilt)

- [x] Spec Tilt dev flow for Photon ✅ `PHOTON_K8S_TILT_DEV.md` committed
- [x] Design `Tiltfile` template ✅ `PHOTON_K8S_TILTFILE_TEMPLATE.md` committed
- [x] Document prerequisites and install flow ✅ `PHOTON_K8S_PREREQS_AND_SETUP.md` committed
- [x] Define `.env` for secrets and profiles ✅ `PHOTON_ENV_DESIGN.md` committed
- [x] Define `.tiltignore` for excluding local dev files ✅ `PHOTON_TILTIGNORE.md` committed
- [ ] Plan `photon dev --target tilt` integration
- [ ] Support auto-reload for frontend/backend during `photon dev`
- [ ] Generate Kind-compatible K8s manifests
- [ ] Enable debugging and log capture

#### Remote Clusters (GKE, EKS, etc)

- [ ] Create base Helm chart for Photon apps
- [ ] Allow `photon deploy --target k8s` to select remote vs local
- [ ] Handle secrets via SecretManager or sealed-secrets
- [ ] Add `kustomize` variant or overlays (optional)
- [ ] Generate Kubernetes manifests: `Deployment`, `Service`, `Ingress`
- [ ] Add CLI command: `photon deploy --target k8s`
- [ ] Document Helm chart or raw YAML options

### General Target Support

- [x] Define supported deployment targets ✅ `PHOTON_DEPLOY_DOCKER_COMPOSE.md` committed
- [ ] Add `--target` CLI flag for build/deploy commands
- [x] Implement deploy strategy for:
    - Docker Compose
    - GitHub Pages
    - Kubernetes

---

## 🧩 CLI & IDE Integration Enhancements

- [ ] Design LSP or CLI protocol extension for build/test status
- [ ] Implement VS Code tasks.json scaffold via `photon init`
- [ ] Define CLI support for `photon status` or `photon watch`
- [ ] Provide inline command help docs via `photon --help <command>`
- [ ] Generate `.vscode/launch.json` and `.vscode/settings.json` for dev convenience

---

## 🧠 Phase 6 – AI Prompt Design

- [ ] Define AI prompt schema and response contract
- [ ] Plan integration with command dispatch and LLM API
- [ ] Define context window + embedding use for spec-based prompting
- [ ] Create fallback & retry strategy for prompt resolution

---

## 🧪 Phase 5 – Test Execution

- [x] Finalize `PHOTON_TEST_STRATEGY.md` and CLI spec for test orchestration
- [ ] Define Photon test strategy across CLI, backend, frontend, and pact
- [ ] Implement `photon test` CLI command with unified test runner
- [ ] Add test manifest discovery for `cargo test`, `vitest`, and `pact verify`
- [ ] Design CI-friendly output (e.g. JUnit or JSON summaries)
- [ ] Plan test filtering by tag, scope, or suite
