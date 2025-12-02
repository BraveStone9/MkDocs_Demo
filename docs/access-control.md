# Access Control Limitations on GitHub Pages

This guide explains the access control behaviour of GitHub Pages and why certain documentation cannot be kept private when using GitHub Free for organizations.

---

## 1. Public Repositories

If a repository is public:

- The GitHub Pages site is also public.
- Anyone with the URL can access the documentation.
- GitHub Pages does not provide built-in restrictions for public sites.

This works well for open documentation but not for internal content.

---

## 2. Private Repositories on GitHub Free for Organizations

GitHub Pages does not support private documentation when the organization is on the **GitHub Free** plan.

Limitations:

- GitHub Pages cannot be enabled for private repositories on the Free plan.
- Access control for Pages (restricting access to organization members) is only available on **GitHub Enterprise Cloud**.

This means:

- If the repo is private → GitHub Pages cannot be used.
- If the repo is public → the Pages site becomes public.

---

## 3. Why This Affects Internal Documentation

Internal documentation normally contains:

- Internal procedures  
- Private APIs  
- Project-specific information  
- Content intended only for employees  

With GitHub Free:

- It is not possible to restrict access to internal documentation.
- Hosting sensitive information publicly is not allowed.

Because of this, documentation that must remain private cannot rely on GitHub Pages.

---

## 4. Summary of the Limitation

| Plan Type                     | Private Pages Support |
|------------------------------|------------------------|
| GitHub Free for Organizations | ❌ Not supported       |
| GitHub Team                  | ❌ Not supported       |
| GitHub Enterprise Cloud      | ✔️ Supported           |

If access needs to be restricted to organization members, GitHub Pages is not a viable option unless the organization upgrades to Enterprise Cloud.

---

## 5. Recommended Next Steps

To keep documentation private:

- Use an internal company machine or VM
- Host the built MKDocs site internally
- Serve it only over VPN or restricted internal networks

Further instructions are provided in the next document.
