# Basic Configuration

Learn how to customize your MkDocs site with essential configuration options.

---

## 1. Site Information

### Basic Site Settings
```yaml
# mkdocs.yml
site_name: My Project Documentation
site_description: A brief description of your project
site_author: Your Name
site_url: https://username.github.io/project-name/
```

### Repository Links
```yaml
repo_url: https://github.com/username/project-name
repo_name: GitHub
edit_uri: edit/main/docs/
```

---

## 2. Theme Configuration

### Material Theme (Recommended)
```yaml
theme:
  name: material
  palette:
    scheme: default
    primary: indigo
    accent: indigo
  features:
    - navigation.tabs
    - navigation.sections
    - toc.integrate
```

### Color Options
- **primary**: indigo, blue, cyan, teal, green, lime, amber, orange, red, pink, purple
- **accent**: Same options as primary

---

## 3. Navigation Structure

### Simple Navigation
```yaml
nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - User Guide: user-guide.md
  - API: api.md
```

### Nested Navigation
```yaml
nav:
  - Home: index.md
  - User Guide:
    - Installation: guide/installation.md
    - Quick Start: guide/quickstart.md
    - Advanced: guide/advanced.md
  - Reference:
    - API: reference/api.md
    - CLI: reference/cli.md
```

---

## 4. Essential Plugins

### Search Plugin (Built-in)
```yaml
plugins:
  - search
```

### Popular Additional Plugins
```yaml
plugins:
  - search
  - git-revision-date-localized:
      type: date
```

Install plugins:
```bash
pip install mkdocs-git-revision-date-localized-plugin
```

---

## 5. Markdown Extensions

### Common Extensions
```yaml
markdown_extensions:
  - admonition
  - codehilite
  - toc:
      permalink: true
  - tables
  - fenced_code
```

### What These Enable
- **admonition**: Call-out boxes (!!! note)
- **codehilite**: Syntax highlighting
- **toc**: Table of contents with permalinks
- **tables**: Table support
- **fenced_code**: Code blocks with ```

---

## 6. Site Extras

### Footer Information
```yaml
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/username
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/username
```

### Copyright Notice
```yaml
copyright: Copyright &copy; 2024 Your Company
```

---

## 7. Complete Example

Here's a complete `mkdocs.yml` for reference:

```yaml
site_name: My Project Docs
site_description: Documentation for my awesome project
site_author: John Doe
site_url: https://johndoe.github.io/my-project/

repo_url: https://github.com/johndoe/my-project
repo_name: GitHub

theme:
  name: material
  palette:
    scheme: default
    primary: blue
    accent: blue
  features:
    - navigation.tabs
    - toc.integrate

nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - API Reference: api.md
  - FAQ: faq.md

plugins:
  - search

markdown_extensions:
  - admonition
  - codehilite
  - toc:
      permalink: true
  - tables

extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/johndoe

copyright: Copyright &copy; 2024 John Doe
```

---

**Next:** Explore [Themes and Customization](themes-customization.md) for advanced styling options.
