# Contributing to Project Name

Thank you for considering contributing to Project Name! This document provides guidelines and instructions for contributing.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Features](#suggesting-features)
- [Pull Request Process](#pull-request-process)
- [Development Setup](#development-setup)
- [Coding Standards](#coding-standards)
- [Testing](#testing)
- [Documentation](#documentation)

## Code of Conduct

This project follows the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to uphold this code. Please report unacceptable behavior to [email@example.com](mailto:email@example.com).

## Getting Started

1. Fork the repository
2. Clone your fork: `git clone https://github.com/yourusername/projectname`
3. Create a branch: `git checkout -b feature/your-feature-name`
4. Make your changes
5. Test your changes
6. Commit your changes: `git commit -m "Add feature description"`
7. Push to your fork: `git push origin feature/your-feature-name`
8. Open a pull request

## How to Contribute

### Types of Contributions

We welcome:
- Bug fixes
- New features
- Documentation improvements
- Performance improvements
- Test coverage improvements
- Examples and tutorials
- Translations

### Before Contributing

- Check existing issues and PRs to avoid duplicates
- For major changes, open an issue first to discuss
- Make sure tests pass
- Follow our coding standards
- Update documentation as needed

## Reporting Bugs

### Before Reporting

- Check if the bug has already been reported
- Verify the bug exists in the latest version
- Collect information about your environment

### Bug Report Template

```markdown
**Describe the bug**
A clear description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Run command '...'
2. With configuration '...'
3. See error

**Expected behavior**
What you expected to happen.

**Actual behavior**
What actually happened.

**Environment**
- OS: [e.g., Ubuntu 22.04]
- Version: [e.g., v1.2.3]
- Go version: [e.g., 1.21.0]

**Additional context**
Any other relevant information.
```

## Suggesting Features

### Before Suggesting

- Check if the feature has already been requested
- Consider if it fits the project scope
- Think about how it would benefit users

### Feature Request Template

```markdown
**Problem Statement**
What problem does this feature solve?

**Proposed Solution**
How would you implement this feature?

**Alternatives Considered**
What other approaches did you consider?

**Use Cases**
Who would use this feature and how?

**Additional Context**
Any other relevant information.
```

## Pull Request Process

### PR Checklist

Before submitting a pull request:

- [ ] Code follows project style guidelines
- [ ] Self-review of code completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] Tests added/updated and passing
- [ ] CHANGELOG.md updated
- [ ] Commits are clear and descriptive
- [ ] Branch is up to date with main

### PR Template

```markdown
## Description

Brief description of changes.

## Related Issue

Fixes #123 (if applicable)

## Type of Change

- [ ] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (fix or feature causing existing functionality to break)
- [ ] Documentation update

## Testing

How was this tested?

## Checklist

- [ ] Code follows style guidelines
- [ ] Self-reviewed code
- [ ] Commented complex code
- [ ] Updated documentation
- [ ] Added tests
- [ ] Tests pass
- [ ] Updated CHANGELOG.md
```

### Review Process

1. Maintainer reviews PR
2. Feedback provided if changes needed
3. Contributor addresses feedback
4. Maintainer approves and merges

Expect response within 48-72 hours.

## Development Setup

### Prerequisites

```bash
# Required
- Go 1.21 or later
- Git

# Optional
- Make (for using Makefile)
- Docker (for integration tests)
```

### Setup Instructions

```bash
# Clone the repository
git clone https://github.com/yourorg/projectname
cd projectname

# Install dependencies
go mod download

# Build
go build

# Run tests
go test -v ./...

# Run linter
golangci-lint run
```

### Project Structure

```
.
├── cmd/           # Command-line interface
├── pkg/           # Public libraries
├── internal/      # Private code
├── docs/          # Documentation
├── examples/      # Example code
├── tests/         # Test files
└── scripts/       # Build and utility scripts
```

## Coding Standards

### Go Style

Follow [Effective Go](https://golang.org/doc/effective_go) and the [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments).

### Formatting

```bash
# Format code
go fmt ./...

# Run linter
golangci-lint run
```

### Naming Conventions

- Use camelCase for unexported names
- Use PascalCase for exported names
- Use descriptive variable names
- Avoid abbreviations unless common

### Error Handling

```go
// Good: Return errors, don't panic
func Process(data []byte) error {
    if len(data) == 0 {
        return fmt.Errorf("empty data")
    }
    return nil
}

// Bad: Don't ignore errors
func Process(data []byte) {
    json.Unmarshal(data, &v) // Error ignored
}
```

### Comments

```go
// Package comment describes the package purpose.
package example

// PublicFunction does something important.
// It takes parameter x and returns y.
func PublicFunction(x int) int {
    // Complex logic explanation
    return x * 2
}
```

## Testing

### Writing Tests

```go
func TestFunction(t *testing.T) {
    tests := []struct {
        name    string
        input   int
        want    int
        wantErr bool
    }{
        {"positive", 5, 10, false},
        {"zero", 0, 0, false},
        {"negative", -5, -10, false},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := Function(tt.input)
            if (err != nil) != tt.wantErr {
                t.Errorf("error = %v, wantErr %v", err, tt.wantErr)
                return
            }
            if got != tt.want {
                t.Errorf("got %v, want %v", got, tt.want)
            }
        })
    }
}
```

### Running Tests

```bash
# All tests
go test -v ./...

# With coverage
go test -v -cover ./...

# Specific package
go test -v ./pkg/example/

# Integration tests (if separated by build tag)
go test -v -tags=integration ./...
```

### Test Coverage

- Aim for >70% coverage
- Focus on critical paths
- Include edge cases
- Test error conditions

## Documentation

### Code Documentation

- Document all exported functions, types, and constants
- Include examples for public APIs
- Keep comments up to date with code

### README Updates

Update README.md when adding:
- New features
- Configuration options
- Usage examples
- Requirements

### Changelog

Add entry to CHANGELOG.md under `[Unreleased]`:

```markdown
### Added
- New feature X (#PR-number)

### Fixed
- Bug in Y (#issue-number)
```

## Commit Messages

### Format

```
type(scope): subject

body (optional)

footer (optional)
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `test`: Test changes
- `chore`: Build process or tooling changes

### Examples

```
feat(api): add user authentication endpoint

Implements OAuth 2.0 authentication flow with support for
Google and GitHub providers.

Closes #123
```

```
fix(parser): handle empty input correctly

Fixes panic when parser receives nil input.

Fixes #456
```

## License

By contributing, you agree that your contributions will be licensed under the same license as the project (see [LICENSE](LICENSE)).

## Questions?

- Open an issue with the `question` label
- Start a discussion on [GitHub Discussions](https://github.com/yourorg/projectname/discussions)
- Contact maintainers at [email@example.com](mailto:email@example.com)

## Recognition

Contributors are recognized in:
- [Contributors page](https://github.com/yourorg/projectname/graphs/contributors)
- Release notes
- README acknowledgments (for significant contributions)

Thank you for contributing!
