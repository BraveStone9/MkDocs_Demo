# Tutorials

Welcome to our comprehensive tutorial section! Here you'll find step-by-step guides to help you get the most out of our documentation system.

## Getting Started Tutorials

### Tutorial 1: Setting Up Your Environment

Learn how to set up your development environment and get started with the basics.

**Prerequisites:**
- Basic knowledge of Markdown
- Text editor or IDE
- Web browser

**Steps:**

1. **Install MkDocs**
   ```bash
   pip install mkdocs
   ```

2. **Create a new project**
   ```bash
   mkdocs new my-project
   cd my-project
   ```

3. **Start the development server**
   ```bash
   mkdocs serve
   ```

4. **Open your browser**
   Navigate to `http://127.0.0.1:8000` to see your documentation.

### Tutorial 2: Creating Your First Page

Learn how to create and structure your documentation pages.

**Steps:**

1. **Create a new Markdown file**
   Create `docs/my-first-page.md`

2. **Add content**
   ```markdown
   # My First Page
   
   This is my first documentation page!
   
   ## Section 1
   Add your content here.
   ```

3. **Update navigation**
   Edit `mkdocs.yml` to include your new page:
   ```yaml
   nav:
     - Home: index.md
     - My First Page: my-first-page.md
   ```

## Advanced Tutorials

### Tutorial 3: Adding Code Examples

Learn how to include and format code examples in your documentation.

**Inline Code:**
Use backticks for `inline code` within sentences.

**Code Blocks:**
```python
def hello_world():
    print("Hello, World!")
    return "Welcome to our documentation!"
```

**Code with Line Numbers:**
```python linenums="1"
def calculate_sum(a, b):
    """Calculate the sum of two numbers."""
    result = a + b
    print(f"The sum of {a} and {b} is {result}")
    return result
```

### Tutorial 4: Working with Images and Media

Learn how to add images and other media to your documentation.

**Adding Images:**
```markdown
![Description](images/example.png)
```

**Image with Caption:**
```markdown
<figure>
  <img src="images/diagram.png" alt="System Architecture" />
  <figcaption>Figure 1: System Architecture Overview</figcaption>
</figure>
```

## Tips and Best Practices

### Writing Effective Documentation

1. **Keep it simple** - Use clear, concise language
2. **Use headings** - Structure content with proper heading hierarchy
3. **Include examples** - Show practical implementations
4. **Test your code** - Ensure all examples work correctly
5. **Update regularly** - Keep content current and relevant

### Markdown Tips

- Use `**bold**` for **important** text
- Use `*italics*` for *emphasis*
- Create lists with `-` or `*`
- Use `>` for blockquotes

> **Pro Tip:** Always preview your changes before publishing to ensure proper formatting.

## Next Steps

Once you've completed these tutorials:

- Explore advanced MkDocs features
- Check out available themes and plugins
- Review our [FAQ](faq.md) for common questions
- Start building your own documentation site!

---

*Ready to dive deeper? Check our [FAQ](faq.md) section for additional information.*
