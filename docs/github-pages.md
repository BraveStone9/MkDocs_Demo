# Deploying Documentation to GitHub Pages

This guide explains how to publish MKDocs documentation using GitHub Pages with GitHub Actions.

---

## 1. Enable GitHub Pages

Open your GitHub repository.

Go to:

**Settings → Pages → Build and Deployment**

Set **Source** to:

```
GitHub Actions
```

This allows GitHub Actions to deploy your documentation automatically.

---

## 2. Create the GitHub Actions Workflow

In your project, create the file:

```
.github/workflows/deploy-mkdocs.yml
```

Add the following content:

```yaml
name: Deploy MKDocs site

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Install dependencies
        run: |
          pip install mkdocs mkdocs-material

      - name: Build MKDocs site
        run: mkdocs build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: "./site"

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Commit and push:

```bash
git add .github/workflows/deploy-mkdocs.yml
git commit -m "Add GitHub Pages workflow"
git push
```

---

## 3. Automatic Deployment

After pushing to the `main` branch:

1. GitHub Actions builds the documentation  
2. The built site is uploaded  
3. GitHub Pages hosts it automatically  

The site URL appears under:

**Settings → Pages**

---

## 4. Ignore the Build Folder

Add this to `.gitignore`:

```
site/
```

The `site` folder is generated automatically during deployment and should not be committed.
