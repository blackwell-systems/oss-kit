# Blackwell OSS Kit

A small, opinionated collection of standards, templates, and checklists for shipping trustworthy open source repositories.

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

Most repos fail because the basics are missing or inconsistent:
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

## Philosophy

This kit intentionally avoids heavy policy.
It assumes:

- one or a few maintainers
- fast iteration
- minimal governance until adoption demands more

The goal is to reduce friction, not add bureaucracy.

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

**Templates**
- [templates/*.template.md](templates/)

**GitHub Templates**
- [.github/](.github/)

## Maintainer

**Blackwell Systems**
Opinionated, minimal, and built for real-world maintainers.
