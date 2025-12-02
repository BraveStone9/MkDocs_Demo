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

## 2. Preparing the Server

Connect to the internal server:

```bash
ssh youruser@server.internal.company
```

Install required tools:

```bash
sudo apt update
sudo apt install git python3 python3-venv -y
```

Clone your documentation repository:

```bash
git clone git@github.com:your-org/your-docs-repo.git
cd your-docs-repo
```

Create a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install MKDocs:

```bash
pip install mkdocs mkdocs-material
```

---

## 3. Building the Documentation

Run the MKDocs build command:

```bash
mkdocs build
```

This generates a static site inside the `site/` folder.

---

## 4. Organizing the Static Files

Create a central folder to host all documentation sites:

```bash
mkdir -p /home/docs
```

Copy the built site to its own subfolder (example: "wave"):

```bash
mkdir -p /home/docs/wave
cp -r site/* /home/docs/wave/
```

Repeat for other documentation projects if needed.

Folder example:

```
/home/docs/
    wave/
    star/
    nextstep/
```

Each folder contains static HTML files.

---

## 5. Serving the Documentation

The simplest option is to use Python’s built-in HTTP server.

Start the server:

```bash
cd /home/docs
python3 -m http.server 8000
```

Documents can be viewed at:

```
http://server.internal.company:8000/wave/
http://server.internal.company:8000/star/
http://server.internal.company:8000/nextstep/
```

---

## 6. Accessing the Documentation Through SSH

If internal ports are restricted, you can use SSH port forwarding.

On your local machine:

```bash
ssh -L 8000:localhost:8000 youruser@server.internal.company
```

Open in your browser:

```
http://localhost:8000
```

This creates a secure tunnel to the internal server through VPN and SSH.

---

## 7. Optional Improvements

Later, this setup can be enhanced by:

- Running the server as a systemd service  
- Using Nginx or Apache instead of `http.server`  
- Assigning a nicer internal URL  
- Adding SSL if required  

The simplest setup, however, is enough to keep documentation private and accessible only within the company network.
