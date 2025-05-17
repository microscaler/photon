<p align="center">
  <img src="/docs/images/Logo.png" alt="Photon logo" />
</p>

# Photon Web Framework

**Photon** is a coroutine-based Rust web framework that delivers a developer experience inspired by [FastAPI](https://fastapi.tiangolo.com/) and [Loco.rs](https://loco.rs/), but built from the ground up on stackful coroutines using [`may`](https://github.com/Xudong-Huang/may) instead of async/await.

## Key Features

- 🚀 **Coroutine Runtime** — powered by `may` for lightweight green threads and blocking-style code
- 📡 **BRRTRouter** — high-performance OpenAPI-first router with request dispatch and validation
- 🧬 **Lifeguard** — coroutine-safe connection pooling over SeaORM for database access
- 🔧 **OpenAPI Generation** — auto-generated and exported OpenAPI 3.1 spec from route macros
- 🔄 **Project CLI Scaffolding** — Rails-style code generators for projects, models, and routes
- 🔌 **Middleware & Metrics** — coroutine-safe hooks for auth, tracing, and observability
- 📡 **WebSocket Support** — coroutine-native real-time communication with Tungstenite
- 🧵 **Background Tasks** — easy coroutine background job execution and task scheduling
- 🎨 **MiniJinja Templating** — Jinja2-compatible rendering engine for server-side views

## Coroutine-Powered Architecture

Photon uses `may` to provide a sync-style coroutine experience, letting developers write blocking-style handler code without `.await`. This enables a simpler, thread-like mental model while achieving high concurrency and performance.

## Concept and Design

For a deep dive into the concepts and design of Photon, check out the following design documents
- [Photon Design Document](./docs/design.md) - ✅
- [Coroutine Architecture](./docs/coroutine.md) - 🚧
- [Routing and OpenAPI](./docs/routing.md) - 🚧
- [Background Tasks](./docs/background.md) - 🚧 
- [WebSocket Support](./docs/websocket.md) - 🚧
- [Project CLI](./docs/cli.md) - 🚧
- [Middleware and Metrics](./docs/middleware.md) - 🚧
- [Templating](./docs/templating.md) - 🚧
- [Connection Pooling](./docs/pooling.md) - 🚧
- [OpenAPI Generation](./docs/openapi.md) - 🚧
- [Error Handling](./docs/errors.md) - 🚧
- [Testing and Debugging](./docs/testing.md) - 🚧
- [Deployment and Production](./docs/deployment.md) - 🚧
- [Security Considerations](./docs/security.md) - 🚧
- [Performance Tuning](./docs/performance.md) - 🚧
- [Future Roadmap](./docs/roadmap.md) - 🚧
- [Contributing Guide](./docs/contributing.md) - 🚧


### Routing with BRRTRouter

- Fully OpenAPI 3.1-compliant
- OpenAPI spec is the single source of truth for routing
- `operationId`'s map to handler functions
- Path/query/body parameters extracted and validated
- Supports JSON, form, multipart, etc.

### Typed Request Handling

Photon uses macros and custom traits to deserialize and validate input:

- serde for JSON serialization/deserialization
- validator crate integration for input validation
- Optional #[derive(ToSchema)] and OpenAPI generation using utoipa

```rust
#[photon_route(method = "POST", path = "/items/{id}")]
fn create_item(id: u32, body: Json<ItemIn>) -> Result<Json<ItemOut>, HttpError> {
    // automatic param parsing and validation
}
```

### WebSockets
Photon wraps tungstenite for coroutine-safe WebSocket support:

Each WebSocket runs in its own coroutine, allowing concurrent real-time connections without blocking.

```rust
fn handle_ws(ws: PhotonWebSocket) {
    while let Ok(msg) = ws.read_message() {
        ws.write_message(msg).unwrap();
    }
}
```

### Background Tasks
Photon provides coroutine-safe background task execution:

- may::go! and may::coroutine::spawn used internally
- Optional task queues (e.g., Redis) for future scale-out

```rust
spawn_background(move || {
    send_email(user_email);
});
```

### Templating

- MiniJinja for dynamic or preloaded templates
- Rendered in coroutine-safe context
- Simple integration for server-side HTML and emails

```rust
render_template("index.html", &context)?;
```

### Project Scaffolding (CLI)

Rails-like developer workflow using embedded templates and automatic file updates.

```bash
photon new my_project
photon generate scaffold post title:string body:text
```

### Roadmap

- OpenAPI-first routing built on top of [BRRTRouter](https://github.com/microscaler/BRRTRouter) integration
  - JSON input/output with validation
- Coroutine-aware connection pooling [Lifeguard](https://github.com/microscaler/lifeguard)
- Project CLI + code scaffolding
- Middleware support
- Static & dynamic assets
- Production-ready metrics & tracing

### License

Photon is licensed under the Apache License Version 2.0, January 2004 and  [MIT License](LICENSE).
