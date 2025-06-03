# 🎨 `photon ui generate form` Command Specification

## 🧭 Purpose

Generates a SolidJS form component from an existing OpenAPI schema. The form supports:

- Two-way binding via `createSignal`
- Field validation based on schema constraints
- Type-safe data model
- Submission handler stub (e.g. `POST /model`)

---

## 📝 Usage

```bash
photon ui generate form <SchemaName>
```

### Example

```bash
photon ui generate form User
```

---

## 📁 Output Files

### `ui/components/UserForm.tsx`

```tsx
import { createSignal } from 'solid-js';

export function UserForm() {
  const [name, setName] = createSignal('');
  const [email, setEmail] = createSignal('');
  const [age, setAge] = createSignal(0);

  const handleSubmit = async (e: Event) => {
    e.preventDefault();
    const user = { name: name(), email: email(), age: age() };
    // TODO: Send to backend
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>Name</label>
      <input value={name()} onInput={e => setName(e.currentTarget.value)} />

      <label>Email</label>
      <input type="email" value={email()} onInput={e => setEmail(e.currentTarget.value)} />

      <label>Age</label>
      <input type="number" value={age()} onInput={e => setAge(parseInt(e.currentTarget.value))} />

      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## ⚙️ Flags

| Flag            | Description                              |
|-----------------|------------------------------------------|
| `--page`        | Generate full page (not just component)  |
| `--route /path` | Link form to a specific backend endpoint |
| `--no-validate` | Skip client-side validation              |
| `--style`       | Specify styling framework (default: tailwind) |

---

## 🧠 Smart Features

- Infers form field types from schema
- Auto-generates labels and inputs with matching `name`
- Adds validation attributes (e.g. `required`, `min`, `format`)
- Handles known formats: `email`, `date`, `password`, `uri`

---

## 📁 File Placement

- Forms go in `ui/components/`
- Optionally generate linked page in `ui/pages/` if `--page` used
- Shared client fetch logic goes in `ui/lib/api.ts`

---

## 🧪 Dev Experience

After running:

```bash
photon ui generate form User
```

You get a drop-in component to:

- Render a typed, reactive form
- Wire to your backend via fetch
- Extend styling and validation immediately

---

## 🔄 Next Steps

- Build OpenAPI parser to map schemas to inputs
- Integrate with Tailwind + Vite
- Add schema validation feedback
- Hook up to `photon generate model` for auto form sync
