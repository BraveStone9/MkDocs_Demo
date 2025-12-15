# Internal Hosting Options

Simple guide for hosting private documentation on company servers when GitHub Pages isn't suitable.

---

## 1. When to Use Internal Hosting

Use internal hosting when your documentation contains:
- Private company information
- Internal APIs and procedures
- Sensitive technical details
- Employee-only content

---

## 2. Basic Setup

### Server Requirements
- Linux server with SSH access
- Python 3.8+ installed
- Access through company VPN

### Install Dependencies
```bash
ssh user@internal-server
sudo apt update
sudo apt install python3 git -y
```

---

## 3. Simple Hosting Steps

### Clone Your Docs Repository
```bash
git clone https://github.com/your-org/your-docs.git
cd your-docs
```

### Build Static Site
```bash
pip install mkdocs mkdocs-material
mkdocs build
```

### Serve Documentation
```bash
cd site
python3 -m http.server 8000
```

Access at: `http://internal-server:8000`

---

## 4. Multiple Projects

### Organize Multiple Docs
```bash
mkdir /home/docs
cp -r project1/site/* /home/docs/project1/
cp -r project2/site/* /home/docs/project2/
```

### Serve All Projects
```bash
cd /home/docs
python3 -m http.server 8000
```

Access:
- `http://internal-server:8000/project1/`
- `http://internal-server:8000/project2/`

---

## 5. Updating Documentation

### Simple Update Script
```bash
#!/bin/bash
cd /path/to/docs-repo
git pull
mkdocs build
cp -r site/* /home/docs/project-name/
echo "Docs updated"
```

---

## 6. Access Through VPN

If you can't access the server directly:

```bash
# SSH tunnel
ssh -L 8000:localhost:8000 user@internal-server

# Then open: http://localhost:8000
```

---

**This is an advanced topic.** For most use cases, stick with [GitHub Pages Deployment](github-pages.md).