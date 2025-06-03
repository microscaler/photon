# 🌐 GitHub Pages Deployment Strategy

## 🧭 Purpose

Deploy the frontend-only portion of a Photon project (SolidJS) to GitHub Pages for static hosting.

---

## 📝 Usage

```bash
photon build --target github-pages
photon deploy --target github-pages
```

---

## 📁 Output

```plaintext
dist/
├── ui/
│   ├── index.html
│   └── assets/
└── .nojekyll
```

- Contents of `dist/ui/` copied to `gh-pages` branch
- `.nojekyll` added to bypass GitHub’s Jekyll processor

---

## 🔧 `photon.toml` Config

```toml
[deploy]
provider = "github-pages"
branch = "gh-pages"
publish_dir = "dist/ui"
auto_commit = true
```

---

## 🚀 Deployment Flow

1. Build frontend using `vite build`
2. Copy `dist/ui` to a temporary `gh-pages` folder
3. Commit and push to `gh-pages` branch
4. Optionally trigger `gh-pages` action workflow

---

## 🧪 Future Support

- Custom domain (`CNAME`)
- SPA fallback via `404.html` or router rewrite
- GitHub Actions integration (`photon deploy --ci`)

---

Would you like to commit this as `docs/DEPLOY/PHOTON_DEPLOY_GITHUB_PAGES.md` and update the stack accordingly?
