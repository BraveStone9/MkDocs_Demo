# Multi-Project Documentation and Portal Setup

This guide explains how to organize documentation for multiple projects and how to create a single portal page that links to all project-specific documentation sites.  
:contentReference[oaicite:0]{index=0}

---

## 1. Why a Portal Is Needed

When each project has its own MKDocs setup:

- Each documentation site is built separately  
- Each project ends up in its own folder under `/home/docs`  
- Users need to remember different paths such as:
  ```
  http://<server>:8000/gai/
  http://<server>:8000/wave/
  http://<server>:8000/star/
  ```

A central portal allows all documentation to be accessed from one place.

---

## 2. Folder Structure for Multiple Documentation Projects

A recommended structure on the internal server is:

```
/home/docs/
    index.html              ← Portal homepage
    gai/                    ← GAI project docs
    wave/                   ← Wave project docs
    star/                   ← Star project docs
    nextstep/               ← Next Step project docs
```

Each project gets its static MKDocs build copied into its own folder.

---

## 3. Creating a Portal MKDocs Site

Create a dedicated repository or folder for your **portal documentation**.

Run:

```bash
mkdocs new portal
```

Inside `portal/docs/index.md`, add links to all project sites:

```markdown
# Documentation Portal

## Projects

- [GAI Documentation](/gai/)
- [Wave Documentation](/wave/)
- [Star Documentation](/star/)
- [Next Step Documentation](/nextstep/)
```

You may update this list whenever new documentation folders are added.

---

## 4. Build the Portal Site

Inside the portal directory:

```bash
mkdocs build
```

This generates the static site in the `site/` folder.

Copy the portal build into the central hosting directory:

```bash
rsync -av --delete site/ /home/docs/
```

This updates the root of your internal documentation directory.

The portal will now load at:

```
http://<server-ip>:8000/
```

---

## 5. Serving All Docs Using One Port

From the `/home/docs` directory:

```bash
cd /home/docs
python3 -m http.server 8000
```

This serves:

- Portal → `http://<server>:8000/`
- GAI docs → `http://<server>:8000/gai/`
- Wave docs → `http://<server>:8000/wave/`
- Star docs → `http://<server>:8000/star/`
- Etc.

This avoids multiple ports and keeps the system simple.

---

## 6. Development vs. Production Hosting

When editing a specific project’s documentation:

### Development Mode (temporary)

Run MKDocs dev server from the project repo:

```bash
mkdocs serve -a 0.0.0.0:8010
```

Access using:

```
http://localhost:8010/
```

This should be used only for editing and testing, not for long-term hosting.

### Production Hosting (permanent)

Once edits are complete:

1. Stop the dev server  
2. Run:
   ```bash
   mkdocs build
   ```
3. Copy the static site to:
   ```
   /home/docs/<project>/
   ```
4. The static server at `:8000` will immediately reflect the update

This keeps the documentation stable and prevents accidental downtime.

---

## 7. Adding a New Project to the Portal

Whenever you create documentation for a new project:

1. Build its static site  
2. Copy it into `/home/docs/<project-name>/`  
3. Update the portal's `index.md` with a link  
4. Rebuild the portal  
5. Sync the portal build to `/home/docs/`  

This ensures all documentation remains organized in one place.

---

## 8. Summary

- Use **one static server** for all documentation  
- Each project gets its own folder inside `/home/docs`  
- The **portal** links everything together  
- Use `mkdocs serve` only for local development  
- Use `mkdocs build` + `rsync` for production updates  

This structure is easy to maintain and scales well as your documentation grows.
