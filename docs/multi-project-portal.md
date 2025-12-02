# Multi-Project Documentation and Portal Setup

This guide explains how to organize documentation for multiple projects and how to create a single portal page that links to all project-specific documentation sites.

---

## 1. Problem: Separate Documentation Per Repository

When each project has its own MKDocs setup:

- Each documentation site is built separately  
- Each site must be hosted in its own folder  
- Users need multiple URLs to access different project docs  

Example structure:

```
/home/docs/wave/
/home/docs/star/
/home/docs/nextstep/
```

Although this works, it can be difficult for users to discover all available documentation.

---

## 2. Solution: Create a Central Documentation Portal

You can create one small MKDocs site that acts as an **index** or **landing page** for all documentation projects.

This portal:

- Lives in its own repository  
- Builds into `/home/docs/`  
- Provides links to each project's documentation  

Example structure after publishing the portal:

```
/home/docs/index.html        → Portal homepage
/home/docs/wave/             → Wave project docs
/home/docs/star/             → Star project docs
/home/docs/nextstep/         → Next Step docs
```

All project documentation can be accessed from a single URL:

```
http://server.internal.company:8000/
```

---

## 3. Creating the Portal Repository

1. Create a new repository, for example:  
   `company-docs-portal`

2. Inside this repo, initialize MKDocs:

   ```
   mkdocs new .
   ```

3. In the `docs/index.md` file, list links to all documentation:

   ```
   # Documentation Portal

   Welcome. Select a project below.

   ## Projects

   - [Wave](/wave/)
   - [Star](/star/)
   - [Next Step Recommender](/nextstep/)

   ```

4. Build the site:

   ```
   mkdocs build
   ```

5. Copy the build into the main docs folder on the server:

   ```
   rsync -av --delete site/ /home/docs/
   ```

The portal will now appear at the root of your internal docs URL.

---

## 4. Serving Multiple Project Docs from One Server

Start a web server from the documentation root:

```bash
cd /home/docs
python3 -m http.server 8000
```

Documentation is accessible at paths such as:

```
http://server.internal.company:8000/wave/
http://server.internal.company:8000/star/
http://server.internal.company:8000/nextstep/
```

The portal homepage appears at:

```
http://server.internal.company:8000/
```

---

## 5. Benefits of the Portal Approach

- Single entry point for all internal documentation  
- Easy for new team members to find what they need  
- Scales as more projects are added  
- Works with the same internal hosting setup  
- No need for separate servers or ports  

---

## 6. Updating the Portal

When adding a new project:

1. Update the portal’s `index.md`  
2. Build the portal site  
3. Sync it to `/home/docs/`  
4. Add the new project’s built site under `/home/docs/projectname/`

This keeps the entire documentation system organized in one place.
