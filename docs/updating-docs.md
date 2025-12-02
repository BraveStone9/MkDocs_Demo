# Updating Documentation

This guide explains how to keep documentation updated when it is hosted on an internal company server. The goal is to make updates simple and repeatable.

---

## 1. Local Editing Workflow

On your local machine:

1. Open the project in VS Code.
2. Edit Markdown files inside the `docs/` folder.
3. Preview changes locally:

   ```bash
   mkdocs serve
   ```

4. Save and commit changes:

   ```bash
   git add .
   git commit -m "Update documentation"
   git push origin main
   ```

The GitHub repository now contains the updated source files.

---

## 2. Prepare the Server for Updates

On the internal server:

1. Navigate to the cloned repository:

   ```bash
   ssh youruser@server.internal.company
   cd /home/docs-src/your-docs-repo
   ```

2. Activate the virtual environment:

   ```bash
   source .venv/bin/activate
   ```

This ensures the server has the correct tools to rebuild MKDocs.

---

## 3. Deployment Script

To make updates easy, create a script on the server to pull the latest changes and rebuild the site.

Create the file:

```
/home/docs-src/your-docs-repo/deploy_docs.sh
```

Add the following content:

```bash
#!/usr/bin/env bash
set -e

cd /home/docs-src/your-docs-repo

source .venv/bin/activate

echo "Pulling latest changes..."
git pull

echo "Building documentation..."
mkdocs build

echo "Updating public folder..."
rsync -av --delete site/ /home/docs/wave/

echo "Update complete."
```

Make the script executable:

```bash
chmod +x /home/docs-src/your-docs-repo/deploy_docs.sh
```

---

## 4. Running the Update

Whenever documentation is changed and pushed to GitHub:

1. Connect to the server:

   ```bash
   ssh youruser@server.internal.company
   ```

2. Run the script:

   ```bash
   /home/docs-src/your-docs-repo/deploy_docs.sh
   ```

The script will:

- Pull the latest changes  
- Build the MKDocs site  
- Copy the output into the correct public folder  

No manual steps are needed after this.

---

## 5. Optional Automatic Updates

You can automate updates further using one of these options:

### Option A — Cron Job

Add a scheduled task to the server:

```bash
crontab -e
```

Example entry (run every 10 minutes):

```
*/10 * * * * /home/docs-src/your-docs-repo/deploy_docs.sh
```

### Option B — GitHub Actions with SSH

A GitHub Actions workflow can:

- connect to the internal server using SSH  
- execute `deploy_docs.sh` automatically on every push  

This requires SSH keys and internal approval.

---

## 6. Summary

The simplest update flow is:

1. Edit documentation locally  
2. Push changes to GitHub  
3. Run `deploy_docs.sh` on the internal server  

This keeps the internal documentation up-to-date and easy to maintain.
