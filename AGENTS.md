# PlayM8s Documentation Development Guide for Agentic Coding

This guide provides essential information for AI coding agents working with the PlayM8s documentation site, which is built using Hugo with the Lotus Docs theme.

## Project Structure

```
docs/
├── hugo/                 # Main Hugo site
│   ├── archetypes/       # Content templates
│   ├── assets/           # SCSS, JS, and other assets
│   ├── content/          # Markdown content files
│   ├── layouts/          # Custom HTML templates
│   ├── static/           # Static assets
│   ├── public/           # Generated site (do not edit)
│   └── hugo.toml         # Hugo configuration
└── profile/              # Project profile (README)
```

## Build Commands

### Local Development Server
```bash
# Serve locally with live reload
hugo server --source ./hugo

# Serve with draft posts visible
hugo server --source ./hugo --buildDrafts --buildFuture

# Serve on a specific port
hugo server --source ./hugo --port 1313
```

### Production Build
```bash
# Build for production (generates static files in ./hugo/public)
hugo --source ./hugo --gc --minify

# Build with specific base URL
hugo --source ./hugo --gc --minify --baseURL "https://pm8s.io/"
```

## Testing

### Link Checking
```bash
# Check internal links (requires installation of hugo-utils)
hugo utils link-check --source ./hugo
```

### Validation
```bash
# Validate configuration
hugo check --source ./hugo

# Validate front matter
hugo check --source ./hugo frontmatter
```

## Code Style Guidelines

### Markdown Content

1. **Front Matter Format**
   - Use TOML format wrapped in `---`
   - Required fields: title, description, draft
   - Example:
     ```markdown
     ---
     title: "Getting Started"
     description: "Learn how to get started with PlayM8s"
     draft: false
     weight: 1
     ---
     ```

2. **Headings**
   - Use ATX-style headers (# Heading 1, ## Heading 2)
   - Follow proper hierarchy (don't skip levels)
   - Use sentence case (not title case)

3. **Lists**
   - Use hyphens (`-`) for unordered lists
   - Use consistent indentation (2 spaces)
   - Add blank lines before and after lists

4. **Code Blocks**
   - Specify language for syntax highlighting
   - Use proper indentation
   - Example:
     ```markdown
     ```yaml
     apiVersion: v1
     kind: Pod
     ```
     ```

5. **Links**
   - Use relative link text (not "click here")
   - Internal links should be relative to content root
   - External links should include protocol (https://)

### File Organization

1. **Content Structure**
   - `_index.md` for section landing pages
   - Descriptive filenames in kebab-case
   - Logical weight ordering for navigation

2. **Asset Management**
   - Place images in `static/images/` or alongside content
   - Use descriptive filenames
   - Optimize images before committing

### Writing Style

1. **Tone and Voice**
   - Technical but approachable
   - Consistent terminology
   - Active voice preferred

2. **Formatting**
   - Bold for UI elements: **Deploy button**
   - Italics for emphasis: *important note*
   - Backticks for code/commands: `kubectl apply`

3. **Documentation Sections**
   - Overview: Brief introduction to the topic
   - Prerequisites: Requirements before proceeding
   - Steps: Numbered procedures with clear outcomes
   - Examples: Practical demonstrations
   - Troubleshooting: Common issues and solutions

## Theme Specifics

The documentation uses the Lotus Docs theme with Bootstrap SCSS. Key features include:

1. **Shortcodes**
   - `{{< alert >}}` for callouts
   - `{{< tabs >}}` for tabbed content
   - `{{< highlight >}}` for syntax highlighting

2. **Navigation**
   - Automatic sidebar generation from content structure
   - Weight parameter controls ordering
   - Section pages menu configured in hugo.toml

## CI/CD Process

GitHub Actions automatically builds and deploys the site:
- Workflow file: `.github/workflows/hugo.yaml`
- Deploys to GitHub Pages
- Uses Hugo v0.137.1
- Includes minification and garbage collection

## Dependencies

- Hugo v0.137.1 Extended
- Dart Sass for SCSS compilation
- Go modules for theme dependencies

## Common Tasks

### Adding New Content
```bash
# Create new content with archetype template
hugo new --source ./hugo docs/new-page.md
```

### Updating Themes
```bash
# Update theme modules
hugo mod get -u --source ./hugo

# Clean module cache
hugo mod clean --source ./hugo
```

## Linting

There are no specific linters configured for this project. Follow the style guidelines above for consistency.

## Single Test Commands

To test a specific aspect of the documentation:

```bash
# Check internal links only
hugo utils link-check --source ./hugo

# Validate just the configuration
hugo check --source ./hugo

# Build drafts to preview unpublished content
hugo server --source ./hugo --buildDrafts --navigateToChanged
```

## Error Handling

When writing content:

1. Always validate front matter syntax
2. Check that internal links resolve correctly
3. Ensure code examples are syntactically correct
4. Verify that the content builds without warnings

## Naming Conventions

1. **Files**: Use kebab-case (e.g., `getting-started.md`)
2. **Directories**: Use kebab-case (e.g., `custom-resources/`)
3. **Variables in code examples**: Use camelCase or snake_case as appropriate to the language
4. **Configuration keys**: Use camelCase as per Hugo conventions

## Import Guidelines

For Hugo templates and custom layouts:
1. Use Go template syntax appropriately
2. Follow the existing patterns in the `layouts/` directory
3. Reference assets using Hugo's built-in functions
4. Maintain consistency with the Lotus Docs theme patterns

This guide is intended for AI agents working with the codebase and should be updated as the project evolves.