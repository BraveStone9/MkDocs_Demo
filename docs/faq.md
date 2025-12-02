# FAQ
# FAQ

---

## What tools do I need to create documentation?

You need the following:

- Python 3.8 or higher  
- pip  
- Git  
- VS Code  
- MKDocs and a theme such as `mkdocs-material`  

---

## Can I preview the documentation before publishing?

Yes. Use:

```bash
mkdocs serve
```

This starts a local server where you can view changes instantly.

---

## Do I need GitHub to use MKDocs?

No. MKDocs works locally without GitHub.

However:

- GitHub helps with version control  
- GitHub Actions helps automate deployments  
- GitHub Pages is a simple hosting option (public only)

---

## Can GitHub Pages host private documentation?

Not on GitHub Free for organizations.

Private GitHub Pages and access control are only available on **GitHub Enterprise Cloud**.

---

## Why should documentation be hosted internally?

Internal hosting is useful when documentation contains:

- private information  
- internal tooling instructions  
- APIs or workflows not meant for the public  

Internal hosting keeps documentation visible only inside the company network.

---

## How do I update documentation hosted internally?

Update steps:

1. Edit files locally  
2. Push changes to GitHub  
3. Run the update script on the internal server  
4. The built site is refreshed automatically  

This applies to any number of projects.

---

## Can multiple projects share one documentation site?

Yes.

You can build a **documentation portal**, which links to:

- `/wave/`  
- `/star/`  
- `/nextstep/`  
- any other project folders  

This creates a single entry point for all documentation.

---

## Do I need Docker or Nginx?

Not required.

The simplest setup uses:

```bash
python3 -m http.server
```

Docker or Nginx can be added later if needed.

---

## What is the easiest setup overall?

The simplest setup is:

1. Create documentation with MKDocs  
2. Push changes to GitHub  
3. Use an internal server with:
   - a static web folder  
   - one update script  
   - one running HTTP server  
4. Serve all documentation from a single port with different paths  
