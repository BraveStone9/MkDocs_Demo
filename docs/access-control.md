# Access Control Considerations

Quick guide to help you decide between public and private documentation hosting.

---

## 1. GitHub Pages: Public Only

**GitHub Pages makes your documentation public** - anyone with the URL can access it.

✅ **Use GitHub Pages for:**
- Open source projects
- Public API documentation  
- Tutorials and guides
- Portfolio projects

❌ **Don't use GitHub Pages for:**
- Internal company procedures
- Private APIs
- Sensitive technical information
- Employee-only content

---

## 2. Private Documentation Options

If your documentation contains sensitive information, you need alternatives:

### GitHub Enterprise Cloud
- Supports private GitHub Pages
- Expensive (organization upgrade required)
- Access control for organization members

### Internal Hosting
- Host on company servers
- Access through VPN only
- Full control over who can access
- See [Internal Hosting Guide](internal-hosting.md)

---

## 3. Decision Matrix

| Content Type | Recommendation |
|-------------|----------------|
| Open source project | GitHub Pages |
| Public API docs | GitHub Pages |
| Internal procedures | Internal hosting |
| Private company APIs | Internal hosting |
| Employee handbook | Internal hosting |
| Mixed public/private | Separate sites |

---

## 4. Quick Decision

**Ask yourself: "Can this be public on the internet?"**

- **Yes** → Use GitHub Pages
- **No** → Use internal hosting
- **Some parts** → Create separate documentation sites

---

**Need private hosting?** Continue with [Internal Hosting Options](internal-hosting.md).
