# Branch Protection Rulesets

Ready-to-use GitHub branch protection rulesets that can be imported directly into your repository.

## Available Rulesets

### 1. Minimal Protection (`minimal-protection.json`)

**Use for:** Personal projects, learning repos, experiments

**Features:**
- Blocks force pushes to main
- Blocks branch deletion
- Requires pull requests (but allows self-merge)
- No review requirements

**Best for:** Solo developers who want basic safety without bureaucracy.

### 2. Standard Protection (`standard-protection.json`)

**Use for:** Most open source projects

**Features:**
- Blocks force pushes and deletions
- Requires linear history (squash/rebase merging)
- Requires 1 approval on pull requests
- Dismisses stale reviews on new commits
- Requires CI and test checks to pass
- Requires branches to be up to date before merging
- Admins can bypass with pull request

**Best for:** Active open source libraries, tools, and applications.

### 3. Strict Protection (`strict-protection.json`)

**Use for:** Security-critical or production infrastructure projects

**Features:**
- All Standard Protection features
- Applies to both `main` and `release/*` branches
- Requires 2 approvals on pull requests
- Requires signed commits (GPG/SSH)
- Requires code owner approval
- Requires last push approval (no self-merge)
- Additional required checks: security-scan, code-coverage
- No bypass actors (even admins follow rules)

**Best for:** Security tools, financial applications, infrastructure projects.

## How to Use

### Method 1: Import via GitHub UI

1. Go to your repository **Settings** → **Rules** → **Rulesets**
2. Click **New ruleset** → **Import a ruleset**
3. Upload one of the JSON files from this directory
4. Review settings
5. Click **Create**

### Method 2: Import via GitHub CLI

```bash
# Install GitHub CLI if needed
brew install gh

# Authenticate
gh auth login

# Import ruleset
gh api repos/{owner}/{repo}/rulesets \
  --method POST \
  --input rulesets/standard-protection.json
```

### Method 3: Copy/Paste via API

```bash
# Using curl
curl -X POST \
  -H "Authorization: token YOUR_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  https://api.github.com/repos/OWNER/REPO/rulesets \
  -d @standard-protection.json
```

## Customization

After importing, you can customize:

### Change Required Status Checks

Edit the `required_status_checks` array to match your CI workflow:

```json
{
  "type": "required_status_checks",
  "parameters": {
    "required_status_checks": [
      {
        "context": "build",
        "integration_id": null
      },
      {
        "context": "lint",
        "integration_id": null
      },
      {
        "context": "test",
        "integration_id": null
      }
    ]
  }
}
```

Status check names must match your GitHub Actions workflow job names.

### Change Branch Patterns

Apply to different branches:

```json
{
  "conditions": {
    "ref_name": {
      "include": [
        "refs/heads/main",
        "refs/heads/develop",
        "refs/heads/release/*"
      ],
      "exclude": [
        "refs/heads/experimental/*"
      ]
    }
  }
}
```

### Add Bypass Actors

Allow specific roles, teams, or apps to bypass rules:

```json
{
  "bypass_actors": [
    {
      "actor_id": 5,
      "actor_type": "RepositoryRole",
      "bypass_mode": "pull_request"
    },
    {
      "actor_id": 1234,
      "actor_type": "Team",
      "bypass_mode": "always"
    }
  ]
}
```

**Actor types:**
- `RepositoryRole`: 5 (Admin), 4 (Maintain), 2 (Write)
- `Team`: GitHub team ID
- `Integration`: GitHub App ID (e.g., Dependabot)

**Bypass modes:**
- `always`: Can completely bypass rules
- `pull_request`: Must use PR but can self-approve

## Finding Your Status Check Names

To find the exact names of your status checks:

1. Go to a recent pull request
2. Scroll to the checks section
3. Note the exact names (case-sensitive)

Or check your workflow file:

```yaml
# .github/workflows/ci.yml
name: CI  # This is the workflow name

jobs:
  test:  # This is the job name (the status check name)
    runs-on: ubuntu-latest
    steps:
      - run: make test
```

Status check name will be: `test`

## Required Workflows

Before enabling status check requirements, ensure your workflows run on pull requests:

```yaml
# .github/workflows/ci.yml
name: CI

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: make test
```

## Troubleshooting

### "Required status check is not found"

**Solution:** Run the workflow at least once on a pull request to register the check name.

### "Admin cannot bypass protection"

**Solution:** Add admin role to `bypass_actors` or temporarily disable the ruleset.

### "Dependabot PRs are blocked"

**Solution:** Add Dependabot as bypass actor:

```json
{
  "actor_id": 29,
  "actor_type": "Integration",
  "bypass_mode": "pull_request"
}
```

Or use auto-merge workflow (see `docs/branch-protection.md`).

## Testing Before Production

Test on a non-critical branch first:

1. Create test branch: `git checkout -b test-protection`
2. Import ruleset but apply only to `test-protection` branch
3. Test PR workflow
4. Verify all checks work
5. Update ruleset to apply to `main`

## Migration Strategy

### From No Protection

1. Start with **minimal** ruleset
2. Add team workflows for CI/tests
3. After 1-2 weeks, upgrade to **standard**
4. Monitor for issues
5. Adjust as needed

### From Legacy Protection Rules

1. Export existing rules (if possible)
2. Review with team
3. Import new ruleset on test branch
4. Test thoroughly
5. Replace legacy rules with new ruleset

## See Also

- [Branch Protection Guide](../docs/branch-protection.md) - Comprehensive documentation
- [GitHub Rulesets Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets)
- [CODEOWNERS Syntax](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)

---

**Need help?** Open an issue or see our [Support Guide](../templates/SUPPORT.template.md).
