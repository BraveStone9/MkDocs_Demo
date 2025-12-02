# Getting Started with MKDocs

This guide explains how to set up MKDocs on your local machine and prepare it for creating documentation.

---

## 1. Install Required Tools

Make sure you have the following installed:

- Python 3.8 or higher  
- pip (comes with Python)  
- Git  
- VS Code (recommended)

Check installation:

```bash
python --version
pip --version
git --version
```

---

## 2. Create a New MKDocs Project

Create a folder and enter it:

```bash
mkdir mkdocs-demo
cd mkdocs-demo
```

(Optional) Create a virtual environment:

```bash
python -m venv .venv

# Activate it
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
```

Install MKDocs and a theme:

```bash
pip install mkdocs mkdocs-material
```

Initialize the project:

```bash
mkdocs new .
```

This creates:

- `mkdocs.yml` — configuration file  
- `docs/` directory — contains documentation pages

Open the folder in VS Code:

```bash
code .
```

---

## 3. Preview Documentation Locally

Use this command to start a local server:

```bash
mkdocs serve
```

Open the URL shown in the terminal (usually `http://127.0.0.1:8000/`).

Any changes you make in VS Code will reload automatically in the browser.

---

## 4. Initialize Git and Push to GitHub

Initialize a Git repository:

```bash
git init
git add .
git commit -m "Initial MKDocs setup"
```

Create a new repository on GitHub and connect it:

```bash
git remote add origin https://github.com/<username>/<repo>.git
git branch -M main
git push -u origin main
```

You now have MKDocs running locally and stored in a GitHub repository.

