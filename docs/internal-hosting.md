# Internal Hosting on Company Servers

This guide explains how to host MKDocs documentation on an internal company machine instead of GitHub Pages. This approach allows documentation to remain private and accessible only through VPN or internal network access.

---

## 1. Overview

When GitHub Pages cannot be used for private documentation, the documentation can be hosted on:

- A company Linux server  
- An internal virtual machine  
- Any machine accessible through VPN and SSH  

The idea is simple:

1. Clone the documentation repository onto the server  
2. Build the MKDocs site  
3. Serve the static files inside the internal network

Only people inside the VPN or allowed internal network can access the documentation.

---

## 2. Running MKDocs in Development Mode (Temporary)

While editing or testing documentation on the server, you may use the MKDocs development server:

```bash
mkdocs serve -a 0.0.0.0:8010
```

You can access it from a browser on the same server:

```
http://localhost:8010/
```

If ports are allowed on the VPN network, other team members can access it as:

```
http://<server-ip>:8010/
```

### Notes

- This is intended only for **temporary preview**
- The development server should not be used for permanent hosting
- Once development is complete, switch to a **static build**

---

## 3. Building the Documentation (Static Site)

To move from the development server to a stable hosted version:

```bash
mkdocs build
```

This generates a static site in the `site/` directory.

The static version is more stable and safer to serve internally.

---

## 4. Central Documentation Folder

Create a central folder to host all documentation sites:

```bash
mkdir -p /home/docs
```

Inside it, create a subfolder for each project:

```bash
mkdir -p /home/docs/gai
```

Copy the built site into this location:

```bash
rsync -av --delete site/ /home/docs/gai/
```

### Example of a multi-project structure

```
/home/docs/
    gai/
    wave/
    star/
    nextstep/
```

---

## 5. Serving the Documentation (Static Hosting)

Use Python’s simple static file server:

```bash
cd /home/docs
python3 -m http.server 8000
```

Documentation is then available at:

```
http://<server-ip>:8000/gai/
```

If the port is blocked, use SSH port forwarding:

```bash
ssh -L 8000:localhost:8000 user@server
```

Then open:

```
http://localhost:8000/gai/
```

---

## 6. Recommended Hosting Flow

1. Use `mkdocs serve` only for quick previews during editing  
2. Stop the dev server when done  
3. Run `mkdocs build` to generate the static site  
4. Copy the static site into `/home/docs/<project>/`  
5. Serve the `/home/docs` folder from one port such as 8000

This keeps all documentation in one place and makes internal hosting stable.