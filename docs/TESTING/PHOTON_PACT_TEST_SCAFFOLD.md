# 🧪 Pact Test Scaffold Generator (`photon generate pact-test`)

---

## 🧭 Purpose

To quickly scaffold a runnable integration test that exercises an OpenAPI operation, using real HTTP calls and asserting expected Pact-compatible responses.

---

## 📝 Usage

```bash
photon generate pact-test <operationId>
```

Optional flags:
```bash
--path /users/{id}
--method GET
--output tests/users_get.rs
```

---

## 📦 Output Example

### `tests/users_get.rs`
```rust
#[tokio::test]
async fn get_user_contract_test() {
    let client = reqwest::Client::new();
    let res = client
        .get("http://localhost:3000/users/123")
        .send()
        .await
        .unwrap();

    assert_eq!(res.status(), 200);
    let body: serde_json::Value = res.json().await.unwrap();
    assert_eq!(body["id"], "123");
    assert!(body["email"].is_string());
}
```

---

## 📄 Inputs

- `openapi.yaml`
    - operationId must resolve
    - pulls example request/response data
- `photon.toml`
    - determines base URL and testing strategy

---

## 🧠 Smart Features

- Auto-patch missing examples in `openapi.yaml` (if `--fix`)
- Validates test structure against OpenAPI schema
- Supports snapshot-style testing in future (`insta`, etc.)

---

Shall we commit this as `docs/TESTING/PHOTON_PACT_TEST_SCAFFOLD.md`?
