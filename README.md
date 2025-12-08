# Blackwell OSS Kit

> **Open source project templates, best practices, and GitHub repository standards for maintainers**

[![Blackwell Systems™](https://raw.githubusercontent.com/blackwell-systems/blackwell-docs-theme/main/badge-trademark.svg)](https://github.com/blackwell-systems)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Sponsor](https://img.shields.io/badge/Sponsor-Buy%20Me%20a%20Coffee-yellow?logo=buy-me-a-coffee&logoColor=white)](https://buymeacoffee.com/blackwellsystems)

A collection of **copy/paste templates**, **best practice guides**, and **GitHub rulesets** for shipping professional open source projects. Includes README templates, CHANGELOG formats, CONTRIBUTING guides, SECURITY policies, branch protection rules, and documentation standards.

This repo is designed to be:
- **Fast to adopt** (copy/paste templates in minutes)
- **Low ceremony** (no process theater)
- **Consistent** (predictable structure across repos)
- **Tool-friendly** (ready to be integrated into future scaffolding)

## What This Is

Two things in one place:

1) **Reference**
   Short guides explaining:
   - semantic versioning expectations
   - changelog discipline
   - release hygiene
   - security basics
   - governance options

2) **Templates**
   Drop-in files you can copy into any repo:
   - README
   - CHANGELOG
   - CONTRIBUTING
   - SECURITY
   - SUPPORT
   - ROADMAP
   - GOVERNANCE
   - PR + Issue templates

## Why This Exists

Many open source projects struggle with the basics:
- unclear contribution path
- no security contact
- no release discipline
- no stable versioning rules
- incomplete README expectations

This kit exists to make "good defaults" effortless.

## Quick Use

Copy the templates you want:

```bash
# from your project root
curl -fsSL https://raw.githubusercontent.com/blackwell-systems/blackwell-oss-kit/main/templates/README.template.md -o README.md
curl -fsSL https://raw.githubusercontent.com/blackwell-systems/blackwell-oss-kit/main/templates/CHANGELOG.template.md -o CHANGELOG.md
curl -fsSL https://raw.githubusercontent.com/blackwell-systems/blackwell-oss-kit/main/templates/CONTRIBUTING.template.md -o CONTRIBUTING.md
curl -fsSL https://raw.githubusercontent.com/blackwell-systems/blackwell-oss-kit/main/templates/SECURITY.template.md -o SECURITY.md
```

(Replace `blackwell-systems` with your org/user once published.)

## Suggested "Serious OSS Minimum"

If you want the simplest credible baseline, include:

- README.md
- LICENSE
- CHANGELOG.md
- CONTRIBUTING.md
- SECURITY.md
- Pull request template
- Issue templates

## Documentation with Docsify

For projects that grow beyond a single README, we recommend [Docsify](https://docsify.js.org/) for documentation sites:

### Why Docsify?

- **No build step** - Runs entirely in browser
- **Markdown files** - Keep docs in your repo
- **Zero config** - Works out of the box
- **GitHub Pages ready** - Deploy instantly
- **Themeable** - Easy to brand

### Quick Setup

```bash
# In your project root
mkdir docs
cd docs

# Create docs homepage
cat > README.md << 'EOF'
# Project Documentation

Welcome to the docs!
EOF

# Create index.html
cat > index.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Project Docs</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify@4/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: 'Project Name',
      repo: 'https://github.com/yourorg/yourproject',
      loadSidebar: true,
      subMaxLevel: 2,
    }
  </script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4"></script>
</body>
</html>
EOF

# Create sidebar
cat > _sidebar.md << 'EOF'
- [Home](/)
- [Getting Started](getting-started.md)
- [API Reference](api-reference.md)
EOF

# Serve locally
npx docsify-cli serve docs
# Visit http://localhost:3000
```

### Deploy to GitHub Pages

1. Push `docs/` folder to your repo
2. Go to Settings → Pages
3. Select branch and `/docs` folder
4. Save

Your docs are now live at `https://yourorg.github.io/yourproject/`

### Example Projects Using Docsify

- [Vaultmux](https://blackwell-systems.github.io/vaultmux/) - Multi-vault secret management
- [Dotfiles](https://blackwell-systems.github.io/dotfiles/) - Dotfiles management framework
- This project's documentation (coming soon)

See [Docsify documentation](https://docsify.js.org/#/) for themes, plugins, and advanced features.

## Roadmap

- **v0.1**: Reference + templates
- **v0.2**: Language-specific add-ons (Go, Rust, Python)
- **v0.3**: GitHub Actions snippets (CI + release helpers)
- **v1.0**: Optional integration into a scaffold CLI

## License

Use whatever license you want for your own repos.
This kit's content is intended to be copied and adapted.

## Contents

**Reference**
- [docs/principles.md](docs/principles.md)
- [docs/versioning.md](docs/versioning.md)
- [docs/changelog.md](docs/changelog.md)
- [docs/releases.md](docs/releases.md)
- [docs/governance.md](docs/governance.md)
- [docs/branch-protection.md](docs/branch-protection.md)

**Templates**
- [templates/*.template.md](templates/)

**GitHub Templates**
- [.github/](.github/)

**Branch Protection Rulesets**
- [rulesets/](rulesets/) - Ready-to-import JSON rulesets

## Maintainer

**Blackwell Systems**
Opinionated, minimal, and built for real-world maintainers.
