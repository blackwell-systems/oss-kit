# Release Process Guide

How to release new versions of your open source project reliably and consistently.

## Release Checklist

### Pre-Release

- [ ] All tests passing
- [ ] No critical bugs or security issues
- [ ] Documentation updated
- [ ] CHANGELOG.md updated
- [ ] Version number decided (following semver)
- [ ] Migration guide written (if breaking changes)
- [ ] Examples tested
- [ ] Dependencies reviewed and updated

### Release

- [ ] Update version in code (if applicable)
- [ ] Commit version bump
- [ ] Create git tag
- [ ] Push tag to remote
- [ ] Build and test release artifacts
- [ ] Publish to package registries
- [ ] Create GitHub release with notes
- [ ] Update documentation site

### Post-Release

- [ ] Announce release (blog, social media, mailing list)
- [ ] Monitor for issues
- [ ] Respond to bug reports quickly
- [ ] Update project status/badges
- [ ] Start new [Unreleased] section in CHANGELOG

## Step-by-Step Process

### 1. Prepare the Release

#### Review Changes

```bash
# See commits since last release
git log v1.0.0..HEAD --oneline

# Review diff
git diff v1.0.0..HEAD
```

#### Update Version Number

Depending on your language/framework:

**Go (in code):**
```go
const Version = "1.1.0"
```

**Python (setup.py or pyproject.toml):**
```python
version = "1.1.0"
```

**Node.js (package.json):**
```json
{
  "version": "1.1.0"
}
```

**Rust (Cargo.toml):**
```toml
[package]
version = "1.1.0"
```

#### Update CHANGELOG.md

Move entries from `[Unreleased]` to new version section:

```markdown
## [Unreleased]

## [1.1.0] - 2025-12-08

### Added
- New feature X

### Fixed
- Bug in Y
```

Add comparison link at bottom:
```markdown
[1.1.0]: https://github.com/user/repo/compare/v1.0.0...v1.1.0
```

### 2. Commit Changes

```bash
# Commit version bump and changelog
git add .
git commit -m "Prepare release v1.1.0"
```

Commit message formats:
- `Prepare release v1.1.0`
- `Release v1.1.0`
- `Bump version to 1.1.0`

### 3. Create Git Tag

```bash
# Create annotated tag
git tag -a v1.1.0 -m "Release version 1.1.0

- Added feature X
- Fixed bug Y
- Improved performance"

# Or use heredoc for multiline message
git tag -a v1.1.0 -m "$(cat <<'EOF'
Release version 1.1.0

Major changes:
- Feature X added
- Bug Y fixed
- Performance improvements

See CHANGELOG.md for full details.
EOF
)"

# Verify tag
git tag -l v1.1.0
git show v1.1.0
```

### 4. Push to Remote

```bash
# Push commit
git push origin main

# Push tag
git push origin v1.1.0

# Or push all tags
git push --tags
```

### 5. Build Release Artifacts

#### Go Binary Releases

```bash
# Build for multiple platforms
GOOS=linux GOARCH=amd64 go build -o dist/myapp-linux-amd64
GOOS=darwin GOARCH=amd64 go build -o dist/myapp-darwin-amd64
GOOS=windows GOARCH=amd64 go build -o dist/myapp-windows-amd64.exe

# Create checksums
cd dist
sha256sum * > checksums.txt
```

#### Using goreleaser

```yaml
# .goreleaser.yml
builds:
  - env:
      - CGO_ENABLED=0
    goos:
      - linux
      - darwin
      - windows
    goarch:
      - amd64
      - arm64
```

```bash
# Release with goreleaser
goreleaser release --clean
```

#### Python Package

```bash
# Build distributions
python -m build

# Upload to PyPI
twine upload dist/*
```

#### Node.js Package

```bash
# Publish to npm
npm publish
```

### 6. Create GitHub Release

#### Via Web Interface

1. Go to repository → Releases → Draft a new release
2. Choose tag: v1.1.0
3. Release title: v1.1.0 or "Version 1.1.0"
4. Description: Copy from CHANGELOG.md
5. Upload binaries (if applicable)
6. Check "Create a discussion for this release" (optional)
7. Publish release

#### Via CLI (gh)

```bash
# Install GitHub CLI
# https://cli.github.com/

# Create release
gh release create v1.1.0 \
  --title "v1.1.0" \
  --notes-file <(sed -n '/## \[1.1.0\]/,/## \[/p' CHANGELOG.md | head -n -1)

# Upload binaries
gh release upload v1.1.0 dist/*
```

### 7. Publish to Package Registries

#### Go Modules

No action needed! Go modules pull from git tags automatically.

Users install with:
```bash
go get github.com/yourorg/repo@v1.1.0
```

#### PyPI (Python)

```bash
# Build
python -m build

# Upload
twine upload dist/*
```

#### npm (Node.js)

```bash
# Ensure version in package.json matches
npm publish
```

#### Docker Hub

```bash
# Build image
docker build -t yourorg/app:1.1.0 .
docker tag yourorg/app:1.1.0 yourorg/app:latest

# Push
docker push yourorg/app:1.1.0
docker push yourorg/app:latest
```

### 8. Update Documentation

#### Documentation Site

If using separate docs site (Read the Docs, GitHub Pages):

```bash
# Update version in docs config
# Build and deploy docs
```

#### README Badges

Update version badge if hardcoded:
```markdown
[![Version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/user/repo/releases)
```

Or use dynamic badge:
```markdown
[![GitHub release](https://img.shields.io/github/v/release/user/repo)](https://github.com/user/repo/releases)
```

### 9. Announce Release

#### GitHub Release Notes

Already done in step 6.

#### Social Media

```
Released v1.1.0 of MyProject!

New features:
• Feature X
• Feature Y

Bug fixes and performance improvements

Download: https://github.com/user/repo/releases/tag/v1.1.0
```

#### Blog Post (for major releases)

```markdown
---
title: "MyProject v2.0.0 Released"
date: 2025-12-08
---

Today we're excited to announce MyProject v2.0.0, a major release with...

## What's New

### Feature X
Description...

### Breaking Changes
Migration guide...

## Getting Started
Installation instructions...
```

#### Mailing List / Discord / Slack

Share release notes with your community.

## Automation

### GitHub Actions

Create `.github/workflows/release.yml`:

```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.21'

      - name: Run tests
        run: go test -v ./...

      - name: Build binaries
        run: |
          GOOS=linux GOARCH=amd64 go build -o dist/myapp-linux-amd64
          GOOS=darwin GOARCH=amd64 go build -o dist/myapp-darwin-amd64
          GOOS=windows GOARCH=amd64 go build -o dist/myapp-windows-amd64.exe

      - name: Create Release
        uses: softprops/action-gh-release@v1
        with:
          files: dist/*
          body_path: CHANGELOG.md
          draft: false
          prerelease: false
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### goreleaser

Install and configure:

```bash
# Install goreleaser
brew install goreleaser

# Initialize config
goreleaser init

# Test locally (dry run)
goreleaser release --snapshot --clean

# Release (when tag pushed)
goreleaser release --clean
```

Add to GitHub Actions:

```yaml
- name: Run GoReleaser
  uses: goreleaser/goreleaser-action@v5
  with:
    version: latest
    args: release --clean
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Versioning Strategy

### Patch Releases (1.0.x)

Frequency: As needed (bug fixes, security patches)

Process:
1. Fix bug on main branch
2. Update CHANGELOG
3. Tag patch version
4. Release

### Minor Releases (1.x.0)

Frequency: Monthly or quarterly

Process:
1. Accumulate features in main branch
2. Code freeze period
3. Testing and bug fixes
4. Update CHANGELOG
5. Tag minor version
6. Release

### Major Releases (x.0.0)

Frequency: Yearly or less

Process:
1. Plan breaking changes
2. Communicate with community
3. Create migration guide
4. Beta testing period
5. Release candidate phase
6. Final release

## Hotfix Process

For critical bugs in production:

```bash
# Create hotfix branch from tag
git checkout -b hotfix/1.0.1 v1.0.0

# Fix bug
git commit -m "Fix critical bug"

# Update CHANGELOG
git commit -m "Update changelog for v1.0.1"

# Tag hotfix
git tag -a v1.0.1 -m "Hotfix release v1.0.1"

# Push
git push origin hotfix/1.0.1
git push origin v1.0.1

# Merge back to main
git checkout main
git merge hotfix/1.0.1
git push origin main
```

## Release Artifacts

### Checksums

Always provide checksums for binaries:

```bash
# Generate SHA256 checksums
sha256sum myapp-* > checksums.txt

# Or use goreleaser (automatic)
```

### Signatures

For security-sensitive projects:

```bash
# Sign release with GPG
gpg --detach-sign --armor myapp-linux-amd64

# Verify
gpg --verify myapp-linux-amd64.asc myapp-linux-amd64
```

## Rolling Back

If a release has critical issues:

```bash
# Delete tag locally
git tag -d v1.1.0

# Delete tag remotely
git push origin :refs/tags/v1.1.0

# Delete GitHub release
gh release delete v1.1.0

# Fix issues, create new release
```

Better approach: Release hotfix version immediately:
- v1.1.0 has bug → Release v1.1.1 with fix

## Best Practices

1. **Test before tagging** - Never tag broken code
2. **Use annotated tags** - Include release notes
3. **Follow semver strictly** - Be predictable
4. **Automate when possible** - Reduce human error
5. **Document breaking changes** - Help users migrate
6. **Sign releases** - Verify authenticity
7. **Provide binaries** - Make installation easy
8. **Update changelog** - Keep history clear
9. **Announce releases** - Inform community
10. **Monitor after release** - Catch issues early

## Common Issues

### Forgot to Update CHANGELOG

Fix in patch release or update GitHub release notes.

### Wrong Version Number

Delete tag and recreate (only if not published to registries).

### Missing Binary

Upload to existing GitHub release.

### Breaking Change in Minor Version

Acknowledge mistake, document workaround, fix in patch.

## Tools

- **GitHub CLI (`gh`)** - Release management
- **goreleaser** - Go release automation
- **twine** - Python package uploads
- **npm** - Node.js package publishing
- **conventional-changelog** - Automated changelog
- **semantic-release** - Fully automated releases

## Resources

- [Semantic Versioning](https://semver.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [GoReleaser](https://goreleaser.com/)
- [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github)

---

A smooth release process builds confidence with users and contributors. Automate where possible, but always test before releasing.
