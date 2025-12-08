# Versioning Guide

How to version your open source project using semantic versioning.

## Semantic Versioning

Format: `MAJOR.MINOR.PATCH` (e.g., `1.4.2`)

### Version Components

**MAJOR** version (1.x.x)
- Increment for incompatible API changes
- Breaking changes to public API
- Removal of deprecated features
- Changes requiring user migration

**MINOR** version (x.1.x)
- Increment for new functionality
- Backward-compatible additions
- New features that don't break existing code
- Deprecation of features (but not removal)

**PATCH** version (x.x.1)
- Increment for bug fixes
- Backward-compatible fixes
- Security patches
- Documentation fixes
- Internal refactoring

### Pre-Release Versions

**Development Phase** (`0.x.x`)
- Major version zero for initial development
- Anything may change at any time
- Not recommended for production use
- Minor version increments can break compatibility

**Alpha** (`1.0.0-alpha.1`)
- Early testing phase
- Feature incomplete
- APIs unstable
- Expect breaking changes

**Beta** (`1.0.0-beta.1`)
- Feature complete
- APIs stabilizing
- Known bugs being fixed
- Limited breaking changes

**Release Candidate** (`1.0.0-rc.1`)
- Ready for release unless bugs found
- No new features
- Final testing phase
- Bug fixes only

## Version Examples

### Starting a Project

```
0.1.0  - Initial release, basic functionality
0.2.0  - Added new features
0.3.0  - More features, some breaking changes
0.9.0  - Feature complete, preparing for 1.0
1.0.0  - First stable release
```

### Stable Project

```
1.0.0  - Stable release
1.0.1  - Bug fix
1.0.2  - Another bug fix
1.1.0  - New feature, backward compatible
1.2.0  - Another feature
2.0.0  - Breaking change, new major version
```

### Pre-Release Cycle

```
1.2.0       - Current stable
2.0.0-alpha.1 - First alpha for v2
2.0.0-alpha.2 - Second alpha
2.0.0-beta.1  - First beta
2.0.0-beta.2  - Second beta
2.0.0-rc.1    - Release candidate
2.0.0-rc.2    - Second RC (bug fixes)
2.0.0         - Stable v2 release
```

## When to Increment

### MAJOR Version

Increment when you:
- Remove public APIs or functions
- Change function signatures
- Alter data formats
- Modify configuration structure
- Break backward compatibility

Examples:
- Removing a function: `func Old()` deleted
- Changing parameters: `func Get(id string)` → `func Get(ctx context.Context, id string)`
- Changing return types: `func Load() error` → `func Load() (Data, error)`

### MINOR Version

Increment when you:
- Add new public APIs or functions
- Add optional parameters
- Add new features
- Deprecate (but don't remove) features
- Make internal improvements

Examples:
- New function: Adding `func NewFeature()`
- New optional field: Adding field to struct with default value
- New method: Adding `String()` method to existing type

### PATCH Version

Increment when you:
- Fix bugs
- Improve performance
- Update documentation
- Refactor internal code
- Fix security issues

Examples:
- Bug fix: Fixing incorrect calculation
- Security patch: Addressing vulnerability
- Documentation: Fixing typos, adding examples

## Tagging Releases

### Git Tags

```bash
# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Push tag to remote
git push origin v1.0.0

# List tags
git tag -l

# Delete tag (if mistake)
git tag -d v1.0.0
git push origin :refs/tags/v1.0.0
```

### Tag Naming

Use `v` prefix:
```
v1.0.0   ✓ Correct
1.0.0    ✗ Avoid
```

Use consistent format:
```
v1.0.0         ✓ Standard
v1.0           ✗ Missing patch
v1.0.0-final   ✗ Unnecessary suffix
```

## Version 0.x.x (Development)

During initial development (0.x.x):

- Major version stays at 0
- Minor version for any breaking changes
- Patch version for compatible changes
- No stability guarantees
- Document as "unstable" or "alpha"

Example progression:
```
0.1.0  - First working version
0.2.0  - Breaking API change
0.2.1  - Bug fix
0.3.0  - Another breaking change
0.9.0  - Pre-release testing
1.0.0  - First stable release
```

## Deprecation Policy

### Marking as Deprecated

1. Add deprecation notice in documentation
2. Add comment in code: `// Deprecated: Use NewFunc instead`
3. Keep function working
4. Provide migration path

```go
// Deprecated: Use NewFunc instead.
// OldFunc will be removed in v2.0.0.
func OldFunc() {
    // Still works
}

// NewFunc replaces OldFunc with better API.
func NewFunc() {
    // New implementation
}
```

### Deprecation Timeline

1. **v1.5.0**: Mark function as deprecated, document alternative
2. **v1.6.0** through **v1.x.x**: Function still works, warnings remain
3. **v2.0.0**: Remove deprecated function

## Breaking Changes

### How to Introduce

1. Document breaking change in CHANGELOG
2. Explain reason for change
3. Provide migration guide
4. Update examples
5. Increment MAJOR version

### Migration Guide Template

```markdown
## Migrating to v2.0.0

### Breaking Changes

#### Function Signature Changed

**Before (v1.x):**
```go
func Connect(host string) error
```

**After (v2.x):**
```go
func Connect(ctx context.Context, host string) error
```

**Migration:**
```go
// Old code:
err := Connect("localhost")

// New code:
ctx := context.Background()
err := Connect(ctx, "localhost")
```

#### Configuration Format Changed

**Before (v1.x):**
```yaml
server: localhost
port: 8080
```

**After (v2.x):**
```yaml
server:
  host: localhost
  port: 8080
```

**Migration:**
Use the included `migrate-config` tool to convert your configuration automatically.
```

## Version Compatibility

### Backward Compatibility

Within same MAJOR version:
- v1.0.0 code works with v1.5.0
- v1.5.0 code may not work with v1.0.0 (uses new features)

Across MAJOR versions:
- v1.x code may not work with v2.x
- Migration required

### Dependency Versioning

```go
// In go.mod
require (
    github.com/yourorg/lib v1.2.3  // Specific version
    github.com/yourorg/lib v1.2    // Any v1.2.x
    github.com/yourorg/lib v1      // Any v1.x.x
)
```

Recommendations:
- Pin to specific version for stability
- Allow minor/patch updates for flexibility
- Test before major version upgrades

## Common Mistakes

### Mistake 1: Breaking Changes in Minor Version

**Wrong:**
```
v1.1.0 - Remove function
```

**Correct:**
```
v2.0.0 - Remove function
```

### Mistake 2: New Features in Patch Version

**Wrong:**
```
v1.0.1 - Add new API endpoint
```

**Correct:**
```
v1.1.0 - Add new API endpoint
```

### Mistake 3: Not Tagging Releases

**Wrong:**
- Commit without tag
- Users clone from main branch

**Correct:**
- Tag every release
- Users download stable versions

### Mistake 4: Inconsistent Tag Format

**Wrong:**
```
v1.0.0
1.0.1
v1.0.2-release
```

**Correct:**
```
v1.0.0
v1.0.1
v1.0.2
```

## Tools

### Version Bump Scripts

```bash
# bump-version.sh
#!/bin/bash
TYPE=$1  # major, minor, or patch
if [ -z "$TYPE" ]; then
    echo "Usage: ./bump-version.sh [major|minor|patch]"
    exit 1
fi

CURRENT=$(git describe --tags --abbrev=0)
echo "Current version: $CURRENT"

# Use semantic versioning tool or manual bump
# Example with semver tool:
# NEW=$(semver bump $TYPE $CURRENT)
# git tag -a "v$NEW" -m "Release v$NEW"
# git push origin "v$NEW"
```

### Automated Versioning

Many projects use:
- `semantic-release` (Node.js)
- `goreleaser` (Go)
- GitHub Actions for automated releases
- Conventional Commits for auto-versioning

## Best Practices

1. **Always use semantic versioning** - Be predictable
2. **Tag every release** - Make versions discoverable
3. **Document breaking changes** - Help users migrate
4. **Test before tagging** - Don't release broken code
5. **Keep CHANGELOG updated** - Track what changed
6. **Deprecate before removing** - Give users time to adapt
7. **Version your dependencies** - Reproducible builds
8. **Consider API stability** - Minimize breaking changes
9. **Use v prefix for tags** - Follow convention
10. **Automate when possible** - Reduce human error

## Resources

- [Semantic Versioning Specification](https://semver.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Go Modules: Version Numbers](https://go.dev/blog/versioning-proposal)
- [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github)

---

Remember: Versions are a contract with your users. Breaking that contract (e.g., breaking changes in minor versions) erodes trust. When in doubt, increment the major version.
