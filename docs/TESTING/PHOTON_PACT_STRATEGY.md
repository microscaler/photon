# 🔬 Pact Strategy for Photon

## 🧭 What is Pact?

Pact is a contract testing framework for ensuring that services agree on their request and response formats. It’s especially useful in microservices and frontend-backend boundaries.

---

## 🎯 Why Pact in Photon?

Photon is OpenAPI-first. This makes it ideal for consumer-driven contract testing, because:

- OpenAPI defines the API shape
- Pact tests verify both consumer expectations and provider implementations
- We can auto-generate many parts of the Pact flow from the spec

---

## ⚙️ What Photon Will Support

### ✅ Pact Consumer Contract Generation

- Generate JSON contracts from OpenAPI examples
- CLI: `photon pact generate-consumer [operationId]`
- Use request/response pairs defined in the spec
- Output path: `pact/consumer/{consumer_name}-{provider_name}.json`

### ✅ Pact Provider Verifier Harness

- Launch a test runner against your own `api/` server
- CLI: `photon pact verify-provider`
- Use JSON contracts from consumer
- Maps to actual handlers using `operationId`

### ✅ Pact Test Scaffold Generator

- CLI: `photon generate pact-test <operationId>`
- Generates:
    - `#[test]` that uses `surf` or `reqwest`
    - Valid request example
    - Expected assertion logic

---

## 📁 Project Structure

```plaintext
pact/
├── consumer/
│   └── web-ui-users-api.json
├── provider/
│   └── verifier.rs
```

---

## 🧩 Integration Points

- OpenAPI `examples` block is the primary source of truth
- Pact CLI is used under the hood
- Photon wraps the config and generation

---

## 🛠️ Design Notes

- Consumer contracts can be committed to Git
- Provider verifier runs in CI/CD
- Pact can be extended later to support message queues, etc.
- Pactflow or CanISend/CanYouHandle may be supported via SaaS later

---

Shall we add this spec as `docs/TESTING/PHOTON_PACT_STRATEGY.md` and continue by designing the generator input structure?
