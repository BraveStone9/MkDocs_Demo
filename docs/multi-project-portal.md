# Multi-Project Documentation

Advanced guide for managing documentation across multiple projects.

---

## 1. When You Need This

Use multi-project documentation when you have:
- Multiple related projects
- Shared components or libraries
- Team working on several repositories
- Need for centralized documentation discovery

---

## 2. Approaches

### Option A: Separate Sites (Recommended)
Each project has its own documentation site:
- `project1.github.io` 
- `project2.github.io`
- `project3.github.io`

**Pros:** Simple, independent deployments  
**Cons:** Users need multiple bookmarks

### Option B: Monorepo Documentation
All docs in one repository with sections for each project.

**Pros:** Single site, unified navigation  
**Cons:** Requires coordination between teams

### Option C: Documentation Portal
Create a landing page linking to all project docs.

---

## 3. Simple Portal Setup

### Create Portal Repository
```bash
mkdocs new company-docs-portal
```

### Portal Index Page
```markdown
# Company Documentation

## Projects

- [Project Alpha](https://team.github.io/project-alpha/)
- [Project Beta](https://team.github.io/project-beta/)
- [Shared Libraries](https://team.github.io/shared-libs/)
```

### Deploy Portal
Deploy like any other MkDocs site to GitHub Pages.

---

## 4. Advanced: Subdomain Organization

For larger organizations:
- `docs.company.com` - Main portal
- `api.company.com` - API documentation  
- `guides.company.com` - User guides

Requires custom domain setup and DNS configuration.

---

**This is an advanced topic.** Most teams should start with separate documentation sites per project and add a portal later if needed.
