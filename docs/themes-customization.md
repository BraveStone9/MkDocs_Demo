# Themes and Customization

Learn how to customize the look and feel of your MkDocs documentation.

---

## 1. Choosing a Theme

### Material Theme (Recommended)
```yaml
theme:
  name: material
```

### Other Popular Themes
```yaml
# Alternative themes
theme:
  name: readthedocs  # Classic look
  name: mkdocs      # Default simple theme
```

Install Material theme:
```bash
pip install mkdocs-material
```

---

## 2. Material Theme Customization

### Color Schemes
```yaml
theme:
  name: material
  palette:
    - scheme: default
      primary: blue
      accent: blue
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

### Available Colors
- **Primary/Accent**: red, pink, purple, indigo, blue, cyan, teal, green, lime, amber, orange, brown, grey, blue-grey

---

## 3. Navigation Features

### Essential Features
```yaml
theme:
  name: material
  features:
    - navigation.tabs        # Top-level tabs
    - navigation.sections    # Collapsible sections
    - navigation.expand      # Expand all sections
    - toc.integrate         # Integrate table of contents
    - search.highlight       # Highlight search terms
```

### Advanced Features
```yaml
theme:
  features:
    - navigation.instant     # Single-page application
    - navigation.tracking    # URL updates with scroll
    - navigation.top         # Back to top button
    - header.autohide        # Hide header on scroll
```

---

## 4. Custom Logo and Favicon

### Add Logo
```yaml
theme:
  name: material
  logo: images/logo.png
  favicon: images/favicon.ico
```

### Text Logo
```yaml
theme:
  name: material
  icon:
    logo: material/library
```

---

## 5. Fonts and Typography

### Font Configuration
```yaml
theme:
  name: material
  font:
    text: Roboto
    code: Roboto Mono
```

### Popular Font Options
- **Text**: Roboto, Open Sans, Lato, Source Sans Pro
- **Code**: Roboto Mono, Fira Code, Source Code Pro

---

## 6. Custom CSS

### Add Custom Styles
Create `docs/stylesheets/extra.css`:
```css
.md-header {
  background-color: #2196F3;
}

.md-tabs {
  background-color: #1976D2;
}
```

Reference in mkdocs.yml:
```yaml
extra_css:
  - stylesheets/extra.css
```

---

## 7. Social Links

### Add Social Icons
```yaml
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/username
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/username
    - icon: fontawesome/brands/linkedin
      link: https://linkedin.com/in/username
```

---

## 8. Complete Theme Example

```yaml
site_name: My Awesome Project
site_description: Beautiful documentation

theme:
  name: material
  palette:
    - scheme: default
      primary: blue
      accent: blue
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
  
  features:
    - navigation.tabs
    - navigation.sections
    - toc.integrate
    - search.highlight
    - navigation.top
  
  font:
    text: Roboto
    code: Roboto Mono
  
  logo: images/logo.png
  favicon: images/favicon.ico

extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/username

extra_css:
  - stylesheets/extra.css

copyright: Copyright &copy; 2024 My Company
```

---

## 9. Testing Your Theme

### Preview Changes
```bash
mkdocs serve
```

### Check Responsiveness
- Test on mobile devices
- Try different screen sizes
- Verify dark/light mode switching

---

**Next:** Learn about [Updating Documentation](updating-docs.md) for maintaining your docs workflow.
