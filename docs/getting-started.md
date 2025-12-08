# Getting Started with MkDocs

This comprehensive guide will get you up and running with MkDocs, whether you're starting fresh or adding documentation to an existing project.

---

## 1. Prerequisites

Ensure you have these tools installed:

### Required Tools
- **Python 3.8 or higher** - [Download from python.org](https://python.org)
- **pip** (included with Python)
- **Git** - [Download from git-scm.com](https://git-scm.com)
- **VS Code** (recommended) - [Download from code.visualstudio.com](https://code.visualstudio.com)

### Verify Installation
```bash
python --version    # Should show 3.8+
pip --version       # Should show pip version
git --version       # Should show git version
```

**Troubleshooting:** If `python` doesn't work, try `python3` on macOS/Linux.

---

## 2. Option A: New MkDocs Project

### Create Project Structure
```bash
mkdir my-project-docs
cd my-project-docs
```

### Set Up Virtual Environment (Recommended)
```bash
# Create virtual environment
python -m venv .venv

# Activate it
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
```

### Install MkDocs
```bash
pip install mkdocs mkdocs-material
```

### Initialize MkDocs
```bash
mkdocs new .
```

This creates:
- `mkdocs.yml` — Configuration file
- `docs/index.md` — Homepage
- `docs/` — Directory for all documentation

---

## 3. Option B: Add MkDocs to Existing Project

If you already have a project repository:

### Navigate to Your Project
```bash
cd /path/to/your/existing/project
```

### Install MkDocs in Project
```bash
# Create virtual environment (recommended)
python -m venv .venv
source .venv/bin/activate  # or .venv\Scripts\activate on Windows

# Install MkDocs
pip install mkdocs mkdocs-material

# Initialize docs
mkdocs new .
```

### Update .gitignore
Add these lines to your `.gitignore`:
```
.venv/
site/
```

---

## 4. Basic Configuration

### Edit mkdocs.yml
Open `mkdocs.yml` and customize:

```yaml
site_name: Your Project Documentation
site_description: Brief description of your project

theme:
  name: material
  palette:
    scheme: default
    primary: blue
    accent: blue

nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - API Reference: api.md

plugins:
  - search

markdown_extensions:
  - codehilite
  - admonition
  - toc:
      permalink: true
```

### Create Additional Pages
```bash
# Create more documentation files
touch docs/getting-started.md
touch docs/api.md
```

---

## 5. Preview Your Documentation

### Start Development Server
```bash
mkdocs serve
```

### Access Documentation
Open your browser to: `http://127.0.0.1:8000`

**Key Features:**
- ✅ **Live reload** - Changes appear instantly
- ✅ **Search functionality** - Built-in search
- ✅ **Mobile responsive** - Works on all devices

### Stop the Server
Press `Ctrl + C` in the terminal

---

## 6. Writing Documentation

### Markdown Basics
```markdown
# Main Heading
## Sub Heading
### Smaller Heading

**Bold text**
*Italic text*

- List item 1
- List item 2

[Link text](https://example.com)

```python
def hello():
    print("Hello, World!")
```
```

### Code Blocks with Syntax Highlighting
````markdown
```python
def calculate(x, y):
    return x + y
```

```bash
pip install package-name
```
````

### Admonitions (Call-out boxes)
```markdown
!!! note "Important Information"
    This is a note that stands out from regular text.

!!! warning
    This is a warning message.

!!! tip
    This is a helpful tip.
```

---

## 7. Version Control Setup

### Initialize Git (if not already done)
```bash
git init
git add .
git commit -m "Initial MkDocs setup"
```

### Connect to GitHub
```bash
# Create repository on GitHub first, then:
git remote add origin https://github.com/yourusername/your-repo.git
git branch -M main
git push -u origin main
```

### Create requirements.txt
```bash
pip freeze > requirements.txt
git add requirements.txt
git commit -m "Add Python dependencies"
git push
```

---

## 8. Common Issues & Solutions

### Python Command Not Found
**Problem:** `'python' is not recognized`
**Solution:** 
- Try `python3` instead of `python`
- Ensure Python is added to PATH during installation

### Virtual Environment Issues
**Problem:** Virtual environment not activating
**Solutions:**
- **Windows:** Use `\.venv\Scripts\activate`
- **PowerShell:** Run `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`
- **macOS/Linux:** Use `source .venv/bin/activate`

### Port Already in Use
**Problem:** `Address already in use`
**Solution:** 
```bash
mkdocs serve -a 127.0.0.1:8001  # Use different port
```

### Theme Not Loading
**Problem:** Default theme appears instead of Material
**Solution:** Ensure `mkdocs-material` is installed:
```bash
pip install mkdocs-material
```

---

## 9. Next Steps

Once you have MkDocs running locally:

1. **📖 Write Content** - Add your project documentation
2. **🚀 Deploy** - Set up [GitHub Pages deployment](github-pages.md)
3. **🎨 Customize** - Explore themes and plugins
4. **👥 Collaborate** - Share with your team

### Useful Resources
- [MkDocs Official Documentation](https://www.mkdocs.org)
- [Material Theme Documentation](https://squidfunk.github.io/mkdocs-material/)
- [Markdown Guide](https://www.markdownguide.org)

---

**🎉 Congratulations!** You now have MkDocs running locally. Ready to deploy? Continue with [GitHub Pages Deployment](github-pages.md).

