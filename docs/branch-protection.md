# Branch Protection Guide

Branch protection rules prevent force pushes, require reviews, and ensure code quality before merging to important branches.

## Why Branch Protection?

**Without protection:**
- Accidental force pushes can delete history
- Untested code can reach main branch
- Multiple people can push conflicting changes
- No review process enforced

**With protection:**
- History is preserved
- Code is reviewed before merging
- Tests must pass
- Consistent quality standards

## Protection Levels

### Minimal (Solo Projects)

For personal projects or small repos with 1-2 contributors:

- Prevent force pushes to main
- Require pull requests (but allow self-merge)
- Optional: Require status checks

**Good for:** Learning projects, experiments, personal tools

### Standard (Team Projects)

For active open source projects with multiple contributors:

- Prevent force pushes and deletions
- Require pull request reviews (at least 1 approval)
- Require status checks (CI, tests)
- Dismiss stale reviews on new commits
- Require linear history (no merge commits)

**Good for:** Most open source projects, libraries, tools

### Strict (Critical Projects)

For production-critical or security-sensitive projects:

- All Standard protections
- Require 2+ reviews for major branches
- Require signed commits
- Require code owner review
- Lock branch (admins can't bypass)
- Require deployment success before merge

**Good for:** Security tools, infrastructure, financial software

## GitHub Branch Protection Setup

### Via Web Interface

1. Go to **Settings** → **Branches**
2. Click **Add branch protection rule**
3. Enter branch name pattern (e.g., `main`, `release/*`)
4. Configure rules (see sections below)
5. Click **Create**

### Via GitHub CLI

```bash
# Install GitHub CLI
brew install gh  # or: https://cli.github.com/

# Authenticate
gh auth login

# Create protection rule
gh api repos/{owner}/{repo}/branches/{branch}/protection \
  --method PUT \
  --input protection-rule.json
```

### Via Rulesets (Recommended)

GitHub's newer rulesets feature provides more flexibility:

1. Go to **Settings** → **Rules** → **Rulesets**
2. Click **New ruleset** → **New branch ruleset**
3. Configure ruleset (see templates below)
4. Click **Create**

**Advantages:**
- Apply to multiple branches with patterns
- Easier to manage across repositories
- Can be imported/exported as JSON
- Better for organization-wide standards

## Standard Protection Rules

### Require Pull Requests

**Settings:**
- Require pull request reviews before merging
- Required approvals: 1 (or 2 for strict)
- Dismiss stale reviews when new commits are pushed
- Require review from code owners (if CODEOWNERS file exists)

**Why:**
- Ensures code review before changes
- Catches bugs and design issues
- Knowledge sharing among team

**Exceptions:**
- Bot PRs (Dependabot, renovate) can auto-merge if tests pass
- Documentation-only changes may not need review

### Require Status Checks

**Common checks:**
- CI pipeline (GitHub Actions, CircleCI)
- Unit tests
- Integration tests
- Linting (golangci-lint, eslint)
- Code coverage
- Security scanning

**Settings:**
- Require status checks to pass before merging
- Status checks required: `ci`, `test`, `lint`
- Require branches to be up to date before merging

**Configuration:**
```yaml
# .github/workflows/ci.yml
name: CI
on:
  pull_request:
    branches: [main]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: make test
```

### Require Linear History

**Settings:**
- Require linear history (squash or rebase merging)

**Options:**
- **Squash merging**: Combine all commits into one
- **Rebase merging**: Replay commits on top of base branch
- **Merge commits**: Allow merge commits (not recommended)

**Recommended:** Squash merging for clean history

### Require Signed Commits

**Settings:**
- Require signed commits

**Why:**
- Verify commit authorship
- Prevent impersonation
- Meet compliance requirements

**Setup:**
```bash
# Generate GPG key
gpg --full-generate-key

# List keys
gpg --list-secret-keys --keyid-format=long

# Get key ID (after sec rsa4096/)
# Add to GitHub: Settings → SSH and GPG keys

# Configure git
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true
```

### Block Force Pushes

**Settings:**
- Do not allow force pushes
- Do not allow deletions

**Why:**
- Prevents accidental history rewriting
- Protects against malicious changes
- Ensures audit trail

**Note:** Admins can still force push if needed (for emergencies)

### Require Conversation Resolution

**Settings:**
- Require conversation resolution before merging

**Why:**
- Ensures all review feedback addressed
- No unresolved questions in merged code
- Clear audit trail of decisions

## Branch Ruleset Templates

### Template 1: Standard Open Source Project

```json
{
  "name": "Protect main branch",
  "target": "branch",
  "enforcement": "active",
  "conditions": {
    "ref_name": {
      "include": ["refs/heads/main"],
      "exclude": []
    }
  },
  "rules": [
    {
      "type": "deletion"
    },
    {
      "type": "non_fast_forward"
    },
    {
      "type": "required_linear_history"
    },
    {
      "type": "pull_request",
      "parameters": {
        "required_approving_review_count": 1,
        "dismiss_stale_reviews_on_push": true,
        "require_code_owner_review": false,
        "require_last_push_approval": false
      }
    },
    {
      "type": "required_status_checks",
      "parameters": {
        "required_status_checks": [
          {
            "context": "ci",
            "integration_id": null
          },
          {
            "context": "test",
            "integration_id": null
          }
        ],
        "strict_required_status_checks_policy": true
      }
    }
  ],
  "bypass_actors": [
    {
      "actor_id": 5,
      "actor_type": "RepositoryRole",
      "bypass_mode": "pull_request"
    }
  ]
}
```

**To import:**
1. Save as `branch-ruleset.json`
2. Go to Settings → Rules → Rulesets
3. Click Import ruleset
4. Upload JSON file

### Template 2: Minimal Protection

```json
{
  "name": "Minimal protection",
  "target": "branch",
  "enforcement": "active",
  "conditions": {
    "ref_name": {
      "include": ["refs/heads/main"],
      "exclude": []
    }
  },
  "rules": [
    {
      "type": "deletion"
    },
    {
      "type": "non_fast_forward"
    },
    {
      "type": "pull_request",
      "parameters": {
        "required_approving_review_count": 0,
        "dismiss_stale_reviews_on_push": false,
        "require_code_owner_review": false,
        "require_last_push_approval": false
      }
    }
  ],
  "bypass_actors": []
}
```

**Use case:** Solo developers who want basic protection but need flexibility

### Template 3: Strict Security Project

```json
{
  "name": "Strict security protection",
  "target": "branch",
  "enforcement": "active",
  "conditions": {
    "ref_name": {
      "include": ["refs/heads/main", "refs/heads/release/*"],
      "exclude": []
    }
  },
  "rules": [
    {
      "type": "deletion"
    },
    {
      "type": "non_fast_forward"
    },
    {
      "type": "required_linear_history"
    },
    {
      "type": "required_signatures"
    },
    {
      "type": "pull_request",
      "parameters": {
        "required_approving_review_count": 2,
        "dismiss_stale_reviews_on_push": true,
        "require_code_owner_review": true,
        "require_last_push_approval": true
      }
    },
    {
      "type": "required_status_checks",
      "parameters": {
        "required_status_checks": [
          {
            "context": "ci",
            "integration_id": null
          },
          {
            "context": "test",
            "integration_id": null
          },
          {
            "context": "security-scan",
            "integration_id": null
          },
          {
            "context": "code-coverage",
            "integration_id": null
          }
        ],
        "strict_required_status_checks_policy": true
      }
    }
  ],
  "bypass_actors": []
}
```

**Use case:** Security-critical projects, financial applications, infrastructure tools

## Release Branch Strategy

### Protect Multiple Branches

Use patterns to protect release branches:

```json
{
  "conditions": {
    "ref_name": {
      "include": [
        "refs/heads/main",
        "refs/heads/release/*",
        "refs/heads/v*"
      ],
      "exclude": []
    }
  }
}
```

### Different Rules for Different Branches

**Main branch:**
- Require 1 review
- All tests must pass
- Squash merging only

**Release branches:**
- Require 2 reviews
- All tests + deployment checks
- No direct pushes (PRs only)

**Feature branches:**
- No protection (fast iteration)
- Require tests to pass before PR

## CODEOWNERS File

Create `.github/CODEOWNERS` to require reviews from specific people:

```
# Default owners for everything
* @maintainer

# Specific paths
/docs/ @documentation-team
/security/ @security-team
*.go @go-team

# Critical files
/go.mod @lead-maintainer
/Dockerfile @devops-team
/.github/ @infrastructure-team
```

**When to use:**
- Large projects with specialized areas
- Security-critical files
- Infrastructure configuration

## Bot Accounts

### Dependabot Auto-Merge

Allow Dependabot to auto-merge if tests pass:

```yaml
# .github/workflows/dependabot-auto-merge.yml
name: Dependabot auto-merge
on: pull_request

permissions:
  pull-requests: write
  contents: write

jobs:
  dependabot:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]'
    steps:
      - name: Enable auto-merge for Dependabot PRs
        run: gh pr merge --auto --squash "$PR_URL"
        env:
          PR_URL: ${{github.event.pull_request.html_url}}
          GH_TOKEN: ${{secrets.GITHUB_TOKEN}}
```

### Bypass Actors

Configure who can bypass protection rules:

```json
{
  "bypass_actors": [
    {
      "actor_id": 5,
      "actor_type": "RepositoryRole",
      "bypass_mode": "pull_request"
    }
  ]
}
```

**Actor types:**
- `RepositoryRole`: Admin, Maintain, Write
- `Team`: GitHub team
- `Integration`: GitHub App (Dependabot, etc.)

**Bypass modes:**
- `always`: Can bypass all rules
- `pull_request`: Must use PR but can self-approve

## Testing Your Protection Rules

### Before Enabling

1. Document current workflow
2. Test on a branch with similar setup
3. Communicate changes to team
4. Have rollback plan

### After Enabling

```bash
# Test force push (should fail)
git push --force origin main

# Test direct push (should fail)
git push origin main

# Test PR workflow (should work)
git checkout -b test-protection
git commit -m "Test"
git push origin test-protection
gh pr create --base main
```

## Common Issues and Solutions

### Issue: "Required status check is not found"

**Problem:** Protection requires a check that doesn't exist

**Solution:**
1. Check workflow names match exactly
2. Ensure workflow runs on pull requests
3. Run workflow at least once to register check

### Issue: "Admin cannot bypass protection"

**Problem:** Need to make emergency fix but rules block it

**Solution:**
1. Temporarily disable enforcement
2. Make fix and push
3. Re-enable protection
4. Or: Use bypass actors in ruleset

### Issue: "Dependabot PRs blocked by protection"

**Problem:** Bot can't merge its own PRs

**Solution:**
- Add Dependabot to bypass actors
- Use auto-merge workflow (see above)
- Or: Configure auto-approval for bot PRs

### Issue: "Too many required reviews slow development"

**Problem:** Waiting for reviews blocks progress

**Solution:**
- Reduce required approvals for most branches
- Use CODEOWNERS for critical paths only
- Allow self-review for documentation
- Set up async review rotation

## Recommendations by Project Size

### Solo Project (1 contributor)
- Block force pushes
- Require pull requests (self-merge allowed)
- Optional: Require tests to pass

### Small Team (2-5 contributors)
- Block force pushes and deletions
- Require 1 review
- Require tests and linting
- Squash merge only

### Medium Project (6-20 contributors)
- All small team rules
- Require up-to-date branches
- Use CODEOWNERS for specialized areas
- Dismiss stale reviews

### Large Project (20+ contributors)
- All medium project rules
- Require 2 reviews for critical branches
- Require signed commits
- Conversation resolution required
- Deployment checks for releases

## Migration Strategy

### From No Protection

1. **Week 1**: Add basic protection (no force push, require PR)
2. **Week 2**: Add required status checks
3. **Week 3**: Add review requirements
4. **Week 4**: Add advanced rules (linear history, signed commits)

### From Legacy Protection

1. Export current rules
2. Review with team
3. Create new ruleset with improvements
4. Test on non-critical branch
5. Apply to main branch
6. Monitor for issues
7. Adjust as needed

## Organization-Wide Policies

For organizations with multiple repos:

### Use Organization Rulesets

1. Go to Organization Settings → Rules → Rulesets
2. Create organization-level ruleset
3. Apply to repositories with patterns
4. Enforce across all repos

### Example Pattern

```json
{
  "name": "Organization standard protection",
  "target": "branch",
  "enforcement": "active",
  "conditions": {
    "repository_name": {
      "include": ["*"],
      "exclude": ["sandbox-*", "test-*"]
    },
    "ref_name": {
      "include": ["refs/heads/main"],
      "exclude": []
    }
  }
}
```

## Checklist

Before going live with branch protection:

- [ ] CI/CD workflows configured and tested
- [ ] Team notified of new rules
- [ ] CODEOWNERS file created (if needed)
- [ ] Bot accounts configured (Dependabot, etc.)
- [ ] Bypass actors identified
- [ ] Emergency procedures documented
- [ ] Rules tested on test branch
- [ ] Rollback plan documented
- [ ] Monitoring set up for failed checks

## Resources

- [GitHub Branch Protection Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches)
- [GitHub Rulesets Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets)
- [CODEOWNERS Syntax](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
- [GitHub CLI](https://cli.github.com/)

---

**Last Updated:** 2025-12-08
**Version:** 1.0
