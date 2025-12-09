# Updating Documentation

Simple workflow for keeping your documentation up-to-date.

---

## 1. Basic Update Workflow

### Local Development
1. **Edit your documentation** files in `docs/`
2. **Preview changes** locally:
   ```bash
   mkdocs serve
   ```
3. **Review** your changes at `http://127.0.0.1:8000`

### Publish Changes
4. **Commit and push** to GitHub:
   ```bash
   git add .
   git commit -m "Update documentation"
   git push origin main
   ```
5. **GitHub Actions** automatically deploys your changes

---

## 2. Testing Before Publishing

### Check for Issues
```bash
# Build and check for errors
mkdocs build --strict
```

### Common Checks
- ✅ All links work correctly
- ✅ Code examples are accurate
- ✅ Images display properly
- ✅ Navigation is logical

---

## 3. GitHub Pages Updates

After pushing to `main` branch:
1. GitHub Actions builds your site
2. Documentation updates automatically
3. Changes are live within 2-3 minutes

### Monitor Deployment
- Check **Actions** tab in your repository
- Watch for build errors or warnings
- Verify changes appear on your live site

---

## 4. Best Practices

### Regular Maintenance
- Update docs when you change code
- Remove outdated information
- Keep screenshots current
- Review and improve clarity

### Collaboration
- Use pull requests for major changes
- Get reviews from team members
- Document your documentation standards
- Keep a changelog for major updates

---

**This covers the essential workflow for keeping your documentation up-to-date.**
