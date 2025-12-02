# Build and Sync Flow for Internal Documentation

This document explains how MKDocs source files from each repository are converted into a static website and how they connect to the central documentation folder located at `/home/docs`.

---

## 1. Overview of the Documentation System

The internal documentation system has **two separate layers**:

### Layer A — Project Repository (Source)
Each project (e.g., `GAI`, `Wave`, `Star`) has its own Git repository that contains:

```
mkdocs.yml
docs/
site/     ← created only after building
```

- `docs/` contains markdown files written by developers.
- `mkdocs.yml` defines navigation, theme, structure.
- Running `mkdocs build` generates a static site in `site/`.

### Layer B — Central Hosting Directory (Served to the network)
The server hosts documentation from a **central folder**:

```
/home/docs/
    gai/
    wave/
    star/
    index.html   ← portal page (optional)
```

This folder is served over a single static server such as:

```bash
cd /home/docs
python3 -m http.server 8000
```

Anything inside these folders becomes accessible inside the VPN at:

```
http://<server>:8000/gai/
http://<server>:8000/wave/
http://<server>:8000/star/
```

---

## 2. What `mkdocs build` Actually Does

Inside a repository (ex: `GAI`):

```bash
mkdocs build
```

This creates or updates:

```
/opt/dev-aditya/GAI/site/
```

The `site/` folder is a **complete static website** containing:

- HTML pages
- CSS + JS files
- Images and assets
- Search index
- Theme files

This folder is **self-contained** and can be copied anywhere — it no longer depends on Python or the repo structure.

---

## 3. How Each Repo Connects to `/home/docs`

After running `mkdocs build`, the build output (`site/`) must be synced into the central hosting directory:

```bash
rsync -av --delete site/ /home/docs/gai/
```

This means:

- `/opt/dev-aditya/GAI/site/` (build output)
    → **copied into**
- `/home/docs/gai/` (served to browser)

The static server reads directly from `/home/docs`, not from the repo.

---

## 4. Why We Use a Central Directory

### Benefits:
- One web server → serves all documentation from different projects
- One URL → multiple paths (`/gai/`, `/wave/`, etc.)
- Cleaner structure than running many ports or servers
- No need to clone every repository inside the web root

### Separation of concerns:
- Repos are for editing and version control  
- `/home/docs` is for hosting finished documentation  

---

## 5. Full Flow When Updating Documentation

### Step 1 — Developer updates docs locally  
```
edit docs/
git add .
git commit -m "Update docs"
git push
```

### Step 2 — Server pulls changes  
```
cd /opt/dev-aditya/GAI
git pull
```

### Step 3 — Build the updated site  
```
mkdocs build
```

### Step 4 — Sync build to hosting folder  
```
rsync -av --delete site/ /home/docs/gai/
```

### Step 5 — Website updates instantly  
Static hosting updates immediately because the files in `/home/docs/gai/` changed.

---

## 6. Summary

- Each project builds its own static site inside its repo (`site/`)
- `/home/docs` hosts the final files served to users
- `mkdocs build` must be run after every change
- Syncing (`rsync`) updates the central hosting directory
- A single server on port 8000 serves all docs

This is the core architecture behind internal hosting.
