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

## 2. How Published Documentation is Updated

### Central Documentation Server
Published documentation is handled by a central documentation server that:

- Retrieves documentation source files from repositories
- Builds static documentation sites using MkDocs  
- Publishes the generated output under a shared documentation portal

### Repository and Branch Structure
Each repository and branch is published to a dedicated path:
- `/gai/main/` - Main branch documentation
- `/gai/superaiassist/` - Feature branch documentation  
- `/project-name/branch-name/` - General pattern

**Note:** Only documentation source files are retrieved for publishing. Application source code is not required.

### When Updates Become Visible
After documentation changes are pushed:
1. The central documentation server fetches the latest documentation sources
2. The site is rebuilt using MkDocs
3. The published content is updated in place

Updates become visible immediately after the publish step completes. **No web server restart is required.**

---

## 3. Testing Before Publishing

### Check for Issues Locally
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

## 4. GitHub Pages Updates

After pushing to `main` branch:
1. **GitHub Actions starts** automatically
2. **Builds your documentation** using MkDocs
3. **Deploys to GitHub Pages**
4. **Changes are live** within 2-3 minutes

### Monitor Deployment
- Check **Actions** tab in your repository
- Watch for build errors or warnings
- Verify changes appear on your live site

---

## 5. Best Practices

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

### Version Control Tips
- Use descriptive commit messages for documentation changes
- Tag important documentation releases
- Keep documentation changes in sync with code changes
- Consider using conventional commit messages

---

**This covers the essential workflow for keeping your documentation up-to-date.**
