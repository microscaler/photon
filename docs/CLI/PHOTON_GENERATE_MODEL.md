# 🧱 `photon generate model` Command Specification

## 🧭 Purpose

Scaffold a complete data model from a single command, generating:

- Rust struct with optional SeaORM integration
- OpenAPI schema component
- SolidJS form component (optional)
- TypeScript client typings (optional)
- Pact contract stub (optional)

---

## 📝 Usage

```bash
photon generate model <ModelName> <field:type>...
```

### Example

```bash
photon generate model User name:string email:string age:int
```

---

## 📁 Output Files

### Backend (`api/src/models/user.rs`)

```rust
use serde::{Deserialize, Serialize};

#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct User {
    pub name: String,
    pub email: String,
    pub age: i32,
}
```

### OpenAPI (`api/openapi.yaml`)

```yaml
components:
  schemas:
    User:
      type: object
      properties:
        name:
          type: string
        email:
          type: string
        age:
          type: integer
```

### Frontend (`ui/components/UserForm.tsx`)

```tsx
import { createSignal } from 'solid-js';

export function UserForm() {
  const [name, setName] = createSignal('');
  const [email, setEmail] = createSignal('');
  const [age, setAge] = createSignal(0);

  const handleSubmit = () => {
    // Handle form submission
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={name()} onInput={(e) => setName(e.currentTarget.value)} />
      <input value={email()} onInput={(e) => setEmail(e.currentTarget.value)} />
      <input type="number" value={age()} onInput={(e) => setAge(parseInt(e.currentTarget.value))} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## ⚙️ Flags

| Flag           | Description                                  |
|----------------|----------------------------------------------|
| `--no-ui`      | Skip generating the SolidJS form component   |
| `--no-client`  | Skip generating the TypeScript client typings|
| `--no-pact`    | Skip generating the Pact contract stub       |
| `--orm`        | Include SeaORM entity and migration files    |

---

## 🧠 Smart Defaults

- Automatically pluralizes model names for collection routes
- Adds CRUD endpoints to the OpenAPI spec
- Generates corresponding route handlers and tests

---

## 🧪 Dev Experience

After running the command:

```bash
photon generate model User name:string email:string age:int
```

You can immediately:

- View the updated OpenAPI spec
- Access the new Rust model in `api/src/models/user.rs`
- Use the generated SolidJS form in your frontend
- Run tests against the new endpoints

---

## 🔄 Next Steps

- Implement the command in the CLI
- Integrate with the OpenAPI spec generator
- Set up templates for the frontend and backend components
- Write tests for the generated code
