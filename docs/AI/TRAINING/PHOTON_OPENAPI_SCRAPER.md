# 🕸️ PHOTON_OPENAPI_SCRAPER.md

## 🧭 Objective

Create a tool that automatically collects real-world OpenAPI specs from public sources (e.g., GitHub, APIs.guru), parses and normalizes them, and prepares structured input for AI training.

---

## 📁 Output Format

Each result will be saved as:

```json
{
  "source": "https://raw.githubusercontent.com/...",
  "path": "/users",
  "method": "get",
  "operation": {
    "summary": "...",
    "operationId": "getUsers",
    ...
  }
}
```

Grouped and versioned by source.

---

## 📦 Sources to Scrape

| Source         | Method                          | Notes                                 |
|----------------|----------------------------------|----------------------------------------|
| GitHub         | GitHub API + query: `openapi.yaml` | Rate-limited, need GitHub token        |
| APIs.guru      | JSON feed of popular public APIs | Great for diversity                    |
| Postman Public | Exported collections with OpenAPI | Convert via Postman CLI                |

---

## 🧰 Tooling Stack (Rust CLI)

- Use `reqwest` or `octocrab` to fetch specs
- Parse and validate with `openapiv3` crate
- Canonicalize path format:
    - Strip unused fields (`description`, `deprecated`)
    - Inline `$ref` where safe
    - Split into path-operation documents

---

## 🧪 Data Curation Rules

- Must contain valid OpenAPI 3.1+ file
- Skip paths missing `operationId` or `responses`
- Normalize tags, methods, summary
- Write per-path JSON file for each valid operation

---

## 🚀 CLI Command (Planned)

```bash
photon dataset scrape --source github --limit 100
```

Flags:
- `--out data/openapi/`
- `--min-methods 5`
- `--dedupe`

---

Want to mark this task in the stack and commit as `PHOTON_OPENAPI_SCRAPER.md`?

