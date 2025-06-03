# 🧪 Photon Pact CLI Commands

---

## `photon pact generate-consumer`

### 🧭 Purpose
Generate a Pact consumer contract from an OpenAPI operation and its examples.

### 📝 Usage
```bash
photon pact generate-consumer <operationId> --consumer web-ui --provider users-api
```

### 🧩 Inputs
- `operationId`: must exist in `openapi.yaml`
- Uses `requestBody.example` and `responses[200].example` or `examples`

### 📦 Output
```plaintext
pact/consumer/web-ui-users-api.json
```

### 🧠 Strategy
- Map OpenAPI examples → Pact `interactions`
- Consumer = source of request
- Provider = your Photon API service

---

## `photon pact verify-provider`

### 🧭 Purpose
Verify a running Photon API instance against recorded Pact contracts.

### 📝 Usage
```bash
photon pact verify-provider --url http://localhost:3000 --provider users-api
```

### 🧩 Inputs
- Contract file from `pact/consumer/*.json`
- Live server URL (running Photon backend)

### 📦 Output
- Console logs of verification results
- Pact log file (optional)

### 🧠 Strategy
- Each interaction in contract is replayed as HTTP request
- Response compared against expected output
- Fails on status/code mismatch or body schema mismatch

---

## Future CLI Ideas
- `photon pact pull --from pactflow`
- `photon pact publish --to pactflow`
- `photon pact diff --between contract1.json contract2.json`
