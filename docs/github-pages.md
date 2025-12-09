# GitHub Pages Deployment

This guide shows you how to automatically deploy your MkDocs documentation to GitHub Pages. This is the **recommended approach** for most projects since it's free, automatic, and works great for public documentation.

---

## 1. When to Use GitHub Pages

✅ **Perfect for:**
- Open source projects
- Public documentation
- Team wikis that can be public
- API documentation
- Tutorial sites

❌ **Not suitable for:**
- Private/confidential documentation
- Internal company procedures
- Sensitive technical information

**Note:** GitHub Pages makes your documentation public. For private documentation, you'll need alternative hosting solutions.

---

## 2. Prerequisites

Before starting, ensure:
- Your project is in a GitHub repository
- You have admin access to the repository
- MkDocs is properly configured locally
- Your documentation builds successfully with `mkdocs build`

---

## 3. Enable GitHub Pages

1. **Open your repository** on GitHub
2. **Navigate to Settings** → **Pages**
3. **Under "Build and deployment"** set:
   - **Source**: `GitHub Actions`

This enables GitHub Actions to automatically build and deploy your docs.

---

## 4. Create the Deployment Workflow

### Step 1: Create the Workflow Directory
In your project root, create:
```bash
mkdir -p .github/workflows
```

### Step 2: Create the Workflow File
Create `.github/workflows/deploy-docs.yml`:

```yaml
name: Deploy Documentation

on:
  push:
    branches: ["main", "master"]
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
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Cache dependencies
        uses: actions/cache@v3
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
          restore-keys: |
            ${{ runner.os }}-pip-

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install mkdocs mkdocs-material
          # If you have additional dependencies:
          # pip install -r requirements.txt

      - name: Build documentation
        run: mkdocs build --strict

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

### Step 3: Commit and Push
```bash
git add .github/workflows/deploy-docs.yml
git commit -m "Add GitHub Pages deployment workflow"
git push origin main
```

---

## 5. Configure Your Site

### Update mkdocs.yml
Add your site URL to `mkdocs.yml`:

```yaml
site_name: Your Project Documentation
site_url: https://yourusername.github.io/your-repo-name/

theme:
  name: material

# ...existing configuration...
```

### Update .gitignore
Ensure your `.gitignore` includes:
```
site/
.venv/
__pycache__/
```

The `site/` folder is built automatically by GitHub Actions.

---

## 6. Deployment Process

After pushing changes to the `main` branch:

1. **GitHub Actions starts** automatically
2. **Builds your documentation** using MkDocs
3. **Deploys to GitHub Pages** 
4. **Your site is live** at `https://yourusername.github.io/your-repo-name/`

### View Deployment Status
- Go to **Actions** tab in your repository
- Click on the latest workflow run
- Monitor the build and deployment progress

---

## 7. Custom Domain (Optional)

### Step 1: Configure DNS
If you own a domain, add a CNAME record:
```
docs.yourcompany.com → yourusername.github.io
```

### Step 2: Add CNAME File
Create `docs/CNAME` with your domain:
```
docs.yourcompany.com
```

### Step 3: Update mkdocs.yml
```yaml
site_url: https://docs.yourcompany.com/
```

### Step 4: Enable HTTPS
In GitHub **Settings** → **Pages**:
- Check "Enforce HTTPS"

---

## 8. Advanced Configuration

### Using requirements.txt
For reproducible builds, create `requirements.txt`:
```
mkdocs==1.5.3
mkdocs-material==9.4.8
# Add other plugins here
```

Update the workflow to use it:
```yaml
- name: Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
```

### Adding Plugins
Example with popular plugins:
```yaml
# In mkdocs.yml
plugins:
  - search
  - git-revision-date-localized
  - minify:
      minify_html: true

# In requirements.txt
mkdocs-git-revision-date-localized-plugin==1.2.1
mkdocs-minify-plugin==0.7.1
```

---

## 9. Troubleshooting

### Build Fails
**Check the Actions tab** for error details:

**Common Issues:**
- Missing dependencies in workflow
- Syntax errors in `mkdocs.yml`
- Broken links in documentation
- Plugin compatibility issues

**Solutions:**
- Use `--strict` flag locally: `mkdocs build --strict`
- Test workflow locally with [act](https://github.com/nektos/act)
- Check plugin documentation for compatibility

### Site Not Updating
**Possible causes:**
- Workflow didn't trigger (check Actions tab)
- Browser cache (try hard refresh: Ctrl+F5)
- DNS propagation (for custom domains)

### Permission Errors
Ensure repository has correct permissions:
- **Settings** → **Actions** → **General**
- **Workflow permissions**: "Read and write permissions"

---

## 10. Best Practices

### Automatic Updates
- Documentation updates automatically on every push to `main`
- Use feature branches for major changes
- Test locally before pushing: `mkdocs serve`

### Branch Protection
Consider protecting your `main` branch:
- **Settings** → **Branches** → **Add rule**
- Require pull request reviews
- Require status checks (including docs build)

### Monitoring
- Watch for build failures in Actions tab
- Set up email notifications for failed builds
- Monitor site performance with GitHub Pages insights

---

## 11. What's Next?

After successful deployment:

1. **Share your documentation URL** with your team
2. **Set up branch protection** for quality control
3. **Consider adding plugins** for enhanced functionality
4. **Monitor and maintain** your documentation

Your documentation is now automatically deployed and updated! 🎉

---

**Need help with private documentation?** Check out [Access Control Considerations](access-control.md) for alternatives to GitHub Pages.
