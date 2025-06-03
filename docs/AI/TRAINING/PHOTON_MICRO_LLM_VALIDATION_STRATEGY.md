# ✅ PHOTON_MICRO_LLM_VALIDATION_STRATEGY.md

## 🧭 Objective

Measure the model’s accuracy, usefulness, and structure compliance when generating OpenAPI paths, schemas, or model definitions.

---

## 📏 Evaluation Goals

| Metric                  | What It Measures                              |
|--------------------------|-----------------------------------------------|
| Valid OpenAPI JSON/YAML | Output parseable by `openapiv3` crate         |
| Prompt-to-output fidelity | Alignment with user intent or prompt         |
| Structure compliance    | Presence of required fields (`operationId`, `responses`) |
| CLI fitness             | Can output be dropped into `openapi.yaml` without edits? |

---

## 🧪 Test Dataset Structure

```json
{
  "instruction": "Create GET /posts",
  "expected.operation.path": "/posts",
  "expected.operation.method": "get",
  "expected.operation.responses.200": "present"
}
```

Can be used with rule-based assertion engine.

---

## 🧰 Test Tools

- `pytest + pydantic` or `jsonschema` for field validation
- Use `openapiv3` crate to parse and re-emit YAML
- Optional: snapshot testing with `insta` in CLI

---

## 🧠 Human Eval Strategy

- Qualitative spot checks:
    - Is this useful for Photon CLI?
    - Would you trust this in a commit?
- Rank outputs across versions

---

## 🏁 Success Thresholds

- >90% output is valid OpenAPI
- >80% responses match intent
- 100% of generated code passes parsing tests

---

Ready to commit as `PHOTON_MICRO_LLM_VALIDATION_STRATEGY.md` and update the stack?
