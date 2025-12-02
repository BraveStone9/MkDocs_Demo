# Updating Documentation

This guide explains the exact steps required to update any project's documentation in the internal system.  
It also explains the full flow from editing the markdown files to updating the central hosting directory.

---

## 1. Two Parts of the Update Process

Documentation updates happen in two phases:

### Phase A — Development (inside the project repository)
You edit markdown files and test them.

### Phase B — Production (update the central `/home/docs` folder)
You build static files and sync them to the hosted directory.

These phases are separate to keep the system clean and stable.

---

## 2. Development Phase (Editing and Testing)

When editing documentation:

1. Open the project repository  
2. Modify the files in `docs/`  
3. Start the MKDocs development server:

   ```bash
   mkdocs serve -a 0.0.0.0:8010
   ```

4. Open in browser:

   ```
   http://localhost:8010/
   ```

5. When done, stop the server:

   ```
   Ctrl + C
   ```

**Important:**  
`mkdocs serve` is only for preview. It does not update the hosted documentation.

---

## 3. Build the Static Site

When your changes are ready:

```bash
mkdocs build
```

This generates the static website inside:

```
site/
```

The `site/` folder contains everything required for hosting.

---

## 4. Update the Central Documentation Folder

Each project has its own folder under `/home/docs`.

For example: **GAI** uses:

```
/home/docs/gai/
```

Sync the new build into this folder:

```bash
rsync -av --delete site/ /home/docs/gai/
```

This immediately replaces the old documentation with the updated version.

---

## 5. How the Website Gets Updated

The static server (running from `/home/docs`) always serves files directly from disk.

Because of this:

- As soon as the files in `/home/docs/gai/` change  
- The website updates automatically  
- No restart is required  
- No extra commands are needed

Example access paths:

```
http://<server>:8000/gai/
http://<server>:8000/wave/
```

---

## 6. Optional: Deployment Script

To make updates easier, create `deploy_docs.sh` inside each project:

```bash
#!/usr/bin/env bash
set -e

cd /opt/dev-aditya/GAI
source .venv/bin/activate

git pull
mkdocs build
rsync -av --delete site/ /home/docs/gai/

echo "Documentation updated."
```

Make it executable:

```bash
chmod +x deploy_docs.sh
```

Now updating docs becomes:

```bash
./deploy_docs.sh
```

---

## 7. Summary

- Edit docs → test with `mkdocs serve`  
- Build docs → `mkdocs build`  
- Sync build → `rsync site/ /home/docs/<project>/`  
- Website updates immediately  
- Use a deploy script to automate these steps  

This is the complete update flow for the internal documentation system.
