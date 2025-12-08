# Frequently Asked Questions

Common questions and solutions for MkDocs beginners.

---

## Getting Started

### Do I need to know Python to use MkDocs?
No. You only need Python installed. All documentation is written in simple Markdown.

### Can I add MkDocs to an existing project?
Yes! Just run `mkdocs new .` in your project root. It won't affect your existing code.

### What's the difference between MkDocs and GitHub Wiki?
- **MkDocs**: Professional themes, better search, version controlled with your code
- **GitHub Wiki**: Simpler but basic styling, separate from your repository

---

## Writing Documentation

### How do I add images?
1. Create `docs/images/` folder
2. Add your image files there  
3. Reference: `![Description](images/screenshot.png)`

### Can I use HTML in Markdown?
Yes, but keep it simple. Stick to Markdown when possible for easier maintenance.

### How do I create code blocks?
Use triple backticks with language name:
````markdown
```python
def hello():
    print("Hello!")
```
````

---

## Deployment & Hosting

### Is GitHub Pages free?
Yes, but documentation becomes public. For private docs, you need GitHub Enterprise or alternative hosting.

### How long does deployment take?
Usually 2-3 minutes after pushing to GitHub. Check the Actions tab for progress.

### Can I use a custom domain?
Yes! Add a `CNAME` file with your domain and configure DNS. See [GitHub Pages docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

### What if my build fails?
Check the **Actions** tab in your repository for error details. Common issues:
- Syntax errors in `mkdocs.yml`
- Missing dependencies
- Broken links (with `--strict` flag)

---

## Themes & Customization

### Which theme should I use?
**Material theme** is recommended for most projects. It's well-maintained and feature-rich.

### How do I change colors?
In `mkdocs.yml`:
```yaml
theme:
  name: material
  palette:
    primary: blue
    accent: blue
```

### Can I add my company logo?
Yes:
```yaml
theme:
  name: material
  logo: images/logo.png
```

---

## Common Issues

### "python: command not found"
- **Windows**: Try `py` instead of `python`
- **Mac/Linux**: Try `python3` instead of `python`
- Ensure Python is in your PATH

### Virtual environment won't activate
- **Windows**: Use `.venv\Scripts\activate`
- **PowerShell**: Run `Set-ExecutionPolicy RemoteSigned` first
- **Mac/Linux**: Use `source .venv/bin/activate`

### Site looks different locally vs deployed
- Clear browser cache (Ctrl+F5)
- Check that `site_url` in `mkdocs.yml` matches your deployment URL
- Ensure all assets use relative paths

### Search not working
Search is automatic with Material theme. If missing:
```yaml
plugins:
  - search
```

---

## Advanced Questions

### Can I have private documentation?
Not with free GitHub Pages. Options:
- GitHub Enterprise Cloud (paid)
- Internal company hosting
- Alternative services (GitLab, Netlify with auth)

### How do I organize large documentation?
- Use nested navigation in `mkdocs.yml`
- Split into logical sections
- Consider separate sites for different audiences
- Use clear, descriptive page titles

### Can I integrate with my API?
Yes, through plugins or custom themes. Popular options:
- OpenAPI documentation generators
- Auto-generated API docs from code comments
- Custom plugins for your specific needs

---

**Still have questions?** Check the [MkDocs documentation](https://www.mkdocs.org) or [Material theme docs](https://squidfunk.github.io/mkdocs-material/).
