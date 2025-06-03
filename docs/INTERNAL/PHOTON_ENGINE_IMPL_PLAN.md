### 🛠️ photon-engine Implementation Plan

#### 📦 Crate Structure

```plaintext
photon-engine/
├── src/
│   ├── lib.rs             # Public API
│   ├── context.rs         # TemplateContext and data types
│   ├── dispatcher.rs      # Mapping from context to templates
│   ├── output.rs          # Write modes, file emit strategy
│   ├── error.rs           # Central error handling
│   └── templates/         # Askama template dir
```

#### 🧩 Entry Points

- `generate_model_files(ctx: TemplateContext) -> GenerationResult`
- `generate_route_handler(ctx: TemplateContext)`
- `generate_ts_client(ctx: TemplateContext)`
- `generate_pact_contract(ctx: TemplateContext)`

All functions return `GenerationResult` (includes written/skipped/conflicted files).

#### 🔄 Output Strategy

- Controlled by `OutputMode`:
    - `Write`
    - `DryRun`
    - `Diff`
    - `Force`
- `HashMap<PathBuf, String>` generated internally, emitted via `output.rs`

#### 🚨 Error Handling

- Unified via `PhotonEngineError` enum
- Covers:
    - Template render errors
    - I/O failures
    - Context validation errors
    - Unsupported schema constructs

#### 🧪 Testing Strategy

- `tests/fixtures/` folder with sample contexts + expected file outputs
- Unit tests for:
    - Dispatcher routing logic
    - Error propagation
    - Template rendering fidelity
- Integration test: `cargo test --workspace`

Would you like this committed as `docs/INTERNAL/PHOTON_ENGINE_IMPL_PLAN.md`?
