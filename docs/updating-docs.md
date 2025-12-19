# Updating Documentation

This page explains how to update documentation and how those updates become visible after publishing.

---

## 1. Documentation Structure

Documentation must exist inside the repository.

Each repository or branch that contains documentation must include:
- `mkdocs.yml`
- a `docs/` folder
- Markdown (`.md`) files inside the `docs/` folder

Example structure:
```text
my-repo/
├── mkdocs.yml
└── docs/
    ├── index.md
    ├── getting-started.md
    └── updating-docs.md
```

Documentation files must always be written in Markdown format (`.md`).

---

## 2. Updating Documentation Locally

### Edit Documentation
- Update existing Markdown files inside `docs/`
- Add new `.md` files if needed
- Update navigation in `mkdocs.yml` when new pages are added

### Preview Changes
Before pushing changes, preview documentation locally:
```bash
mkdocs serve
```

Preview the site at:
```
http://127.0.0.1:8000/
```

---

## 3. Commit and Push Changes

Only documentation source files are required:
- `docs/`
- `mkdocs.yml`

Example:
```bash
git add docs/ mkdocs.yml
git commit -m "docs: update documentation"
git push
```

**Notes:**
- Documentation can be maintained per branch
- Feature branches may have their own documentation
- The generated `site/` folder is not required in the repository

---

## 4. How Published Documentation Is Updated

Published documentation is handled by a central documentation server.

### The Documentation Server:
- Retrieves documentation source files from repositories
- Builds static documentation sites using MkDocs
- Publishes the generated output under a shared documentation portal

### Documentation Publishing Structure
Documentation is published using the following structure:
```
/<repository>/<branch>/
```

**Examples:**
- `/gai/main/`
- `/gai/superaiassist/`

Only documentation files are used for publishing. Application source code is not required.

---

## 5. When Updates Become Visible

After documentation changes are pushed:
1. The documentation server pulls the latest documentation files
2. MkDocs rebuilds the site
3. The updated site is published automatically

The published documentation updates immediately after the build completes. **No manual restart is required.**

---

## 6. Testing Before Publishing

To validate documentation locally:
```bash
mkdocs build --strict
```

### Recommended Checks:
- ✅ Links work correctly
- ✅ Navigation is correct
- ✅ Code examples are accurate
- ✅ Images render properly

---

## 7. Best Practices

- Update documentation alongside code changes
- Keep documentation clear and concise
- Use meaningful commit messages
- Keep documentation structure consistent across repositories

---

**This covers the essential workflow for keeping your documentation up-to-date.**