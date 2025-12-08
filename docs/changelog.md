# Changelog Guide

How to maintain a clear and useful changelog for your project.

## What is a Changelog?

A changelog is a file documenting all notable changes to a project in reverse chronological order (newest first). It helps users and contributors understand what has changed between versions.

## Why Keep a Changelog?

- **Users** need to know if upgrading will break their code
- **Contributors** want to see if their work was included
- **Maintainers** benefit from documented project history
- **Transparency** builds trust with your community

## Format

Follow the [Keep a Changelog](https://keepachangelog.com/) format:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- New feature X

### Changed
- Improved Y

## [1.0.0] - 2025-01-15

### Added
- Initial release
- Feature A
- Feature B

### Fixed
- Bug in component C

[Unreleased]: https://github.com/user/repo/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/user/repo/releases/tag/v1.0.0
```

## Change Categories

### Added
New features or capabilities.

```markdown
### Added
- New `GetUser()` function to retrieve user details
- Support for configuration via environment variables
- Documentation for advanced usage
```

### Changed
Changes to existing functionality.

```markdown
### Changed
- Improved error messages for clarity
- Updated dependencies to latest versions
- Refactored internal module structure
```

### Deprecated
Features marked for removal in future versions.

```markdown
### Deprecated
- `OldFunction()` will be removed in v2.0.0, use `NewFunction()` instead
- Configuration via JSON files, use YAML instead
```

### Removed
Features that were removed in this version.

```markdown
### Removed
- Dropped support for Python 2.7
- Removed deprecated `LegacyAPI` class
- Eliminated unused dependencies
```

### Fixed
Bug fixes.

```markdown
### Fixed
- Fixed crash when input is empty
- Resolved memory leak in cache implementation
- Corrected timezone handling in date parser
```

### Security
Security-related changes, fixes, or improvements.

```markdown
### Security
- Fixed SQL injection vulnerability in search function
- Updated dependency with known security issue
- Added input validation to prevent XSS
```

## Example Changelog

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Configuration validation on startup
- Better error messages for invalid input

### Changed
- Improved performance of list operations

## [2.0.0] - 2025-12-01

### Added
- Support for asynchronous operations
- New `Context` parameter for cancellation
- Integration with external logging systems

### Changed
- **Breaking**: Function signatures now accept `context.Context`
- Renamed `Config` struct fields for clarity
- Updated all dependencies to latest versions

### Removed
- **Breaking**: Dropped support for Go 1.18 and earlier
- Removed deprecated `OldAPI` interface

### Fixed
- Resolved race condition in concurrent access
- Fixed incorrect timeout behavior

### Security
- Updated dependency with CVE-2024-12345

## [1.2.1] - 2025-11-15

### Fixed
- Fixed panic when processing empty arrays
- Corrected documentation typos

## [1.2.0] - 2025-11-01

### Added
- New `Validate()` method for input checking
- Support for custom timeout configuration

### Changed
- Improved logging output format
- Optimized memory usage

## [1.1.0] - 2025-10-15

### Added
- Added `ListAll()` function for batch operations
- New examples in documentation

### Fixed
- Fixed off-by-one error in pagination

## [1.0.0] - 2025-10-01

### Added
- Initial stable release
- Core CRUD operations
- Comprehensive documentation
- Unit and integration tests

[Unreleased]: https://github.com/user/repo/compare/v2.0.0...HEAD
[2.0.0]: https://github.com/user/repo/compare/v1.2.1...v2.0.0
[1.2.1]: https://github.com/user/repo/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/user/repo/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/user/repo/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/user/repo/releases/tag/v1.0.0
```

## Writing Good Entries

### Do: Be Specific

**Good:**
```markdown
- Fixed crash when `GetUser()` receives nil pointer
- Added support for PostgreSQL 15
- Improved startup time by 50% for large datasets
```

**Bad:**
```markdown
- Fixed bug
- Updates
- Performance improvements
```

### Do: Link to Issues/PRs

```markdown
- Fixed memory leak in cache ([#123](https://github.com/user/repo/issues/123))
- Added retry logic ([#456](https://github.com/user/repo/pull/456))
```

### Do: Highlight Breaking Changes

```markdown
### Changed
- **Breaking**: Renamed `Config.Url` to `Config.URL` for consistency
- **Breaking**: Function `Connect()` now returns `(Client, error)` instead of `error`
```

### Do: Credit Contributors

```markdown
- Added dark mode support ([@contributor](https://github.com/contributor))
- Fixed Windows compatibility (thanks @windowsuser)
```

### Don't: Include Every Commit

Not every commit needs a changelog entry. Skip:
- Internal refactoring (unless it affects performance)
- Dependency updates (unless security-related)
- Documentation typo fixes
- CI/build configuration changes

### Don't: Duplicate Release Notes

Keep changelog concise. Detailed technical notes belong in:
- Git commit messages
- Pull request descriptions
- GitHub release notes
- Migration guides

## Workflow Integration

### During Development

1. Add entries to `[Unreleased]` section as you work
2. Commit changelog updates with feature commits
3. Review entries during code review

### During Release

1. Move entries from `[Unreleased]` to new version section
2. Add version number and date
3. Update comparison links at bottom
4. Commit changelog with release tag

### Automation

Some projects use tools to generate changelogs:
- `github-changelog-generator`
- `conventional-changelog`
- `release-drafter` (GitHub Action)

These work best with conventional commits:
```
feat: Add new feature
fix: Fix bug
docs: Update documentation
```

## Multiple Projects

For monorepos with multiple packages:

```markdown
# Changelog

## Package: api

### [2.0.0] - 2025-12-01
- Breaking: New authentication flow

## Package: cli

### [1.5.0] - 2025-12-01
- Added: New `configure` command
```

Or maintain separate CHANGELOG.md in each package directory.

## Best Practices

1. **Update regularly** - Don't let changes pile up
2. **Keep it simple** - Users want summaries, not commit logs
3. **Mark breaking changes** - Make them impossible to miss
4. **Link to details** - Reference issues and PRs
5. **Credit contributors** - Acknowledge community work
6. **Use past tense** - "Added", "Fixed", not "Add", "Fix"
7. **Group by category** - Use standard sections (Added, Changed, etc.)
8. **Newest first** - Most recent version at top
9. **Include dates** - ISO 8601 format (YYYY-MM-DD)
10. **Link to diffs** - Help users see what changed

## Anti-Patterns

### Kitchen Sink

Don't list every tiny change:
```markdown
### Changed
- Fixed typo in comment
- Renamed variable x to y
- Reformatted file
- Updated .gitignore
- Bumped dependency patch version
```

### Vague Entries

Avoid generic descriptions:
```markdown
### Changed
- Various improvements
- Bug fixes
- Performance updates
```

### Commit Log Dumps

Don't copy git log:
```markdown
### Changed
- WIP: trying new approach
- fix typo
- fix typo again
- revert last change
- actually fix it this time
```

## Template

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

### Changed

### Deprecated

### Removed

### Fixed

### Security

## [1.0.0] - YYYY-MM-DD

### Added
- Initial release

[Unreleased]: https://github.com/username/repo/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/username/repo/releases/tag/v1.0.0
```

## Resources

- [Keep a Changelog](https://keepachangelog.com/) - Standard format specification
- [Semantic Versioning](https://semver.org/) - Version numbering guide
- [Conventional Commits](https://www.conventionalcommits.org/) - Commit message format
- [github-changelog-generator](https://github.com/github-changelog-generator/github-changelog-generator) - Automation tool

---

A good changelog is a gift to your future self and your users. It takes minimal effort to maintain and provides immense value when debugging, upgrading, or understanding project history.
