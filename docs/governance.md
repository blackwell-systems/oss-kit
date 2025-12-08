# Governance Guide

How to structure decision-making and maintainership for your open source project.

## Why Governance Matters

Good governance:
- Clarifies who makes decisions
- Prevents contributor conflicts
- Ensures project continuity
- Builds contributor confidence
- Manages project transitions

Bad or absent governance:
- Creates confusion and conflict
- Drives contributors away
- Leads to project abandonment
- Makes succession difficult

## Governance Models

### 1. Benevolent Dictator For Life (BDFL)

**Structure:** Single person makes all final decisions.

**Pros:**
- Fast decision-making
- Clear direction
- Minimal bureaucracy
- Works well for small projects

**Cons:**
- Single point of failure
- Can become bottleneck
- Succession planning difficult
- May discourage contributors

**Best For:**
- Personal projects
- Small libraries
- Early-stage projects
- Strong founding vision

**Example:**
```markdown
## Governance

This project follows a Benevolent Dictator model. [@founder](https://github.com/founder)
makes final decisions on all matters. Contributors are encouraged to discuss proposals
via issues before submitting PRs.
```

**When to Evolve:** When project grows beyond one maintainer's capacity or when you need to step back.

---

### 2. Maintainer Team

**Structure:** Small group of trusted maintainers share decisions.

**Pros:**
- Distributes workload
- Provides redundancy
- Multiple perspectives
- Scales to medium projects

**Cons:**
- Requires coordination
- Potential for disagreement
- Needs conflict resolution process

**Best For:**
- Growing projects
- Active contributors wanting responsibility
- Projects needing multi-timezone coverage

**Example:**
```markdown
## Maintainers

Current maintainers:
- @alice - Lead maintainer
- @bob - Security and releases
- @carol - Documentation and community

Maintainers operate by consensus. Major changes require at least 2 maintainer approvals.
New maintainers nominated by existing maintainers after 3+ significant contributions.
```

**Decision Process:**
- Minor changes: Any maintainer can approve and merge
- Major changes: Require consensus (majority agreement)
- Disputes: Lead maintainer has tie-breaking vote

---

### 3. Consensus-Based

**Structure:** All active contributors participate in decisions.

**Pros:**
- Democratic and inclusive
- Builds strong community
- Diverse perspectives valued

**Cons:**
- Slow decision-making
- Can lead to bikeshedding
- Requires active facilitation

**Best For:**
- Community-driven projects
- Foundation-backed projects
- Projects with diverse stakeholders

**Example:**
```markdown
## Governance

Decisions are made by lazy consensus:
1. Proposal posted as issue or RFC
2. Discussion period (minimum 7 days)
3. If no objections, proposal accepted
4. Objections must be addressed or proposal modified

Major changes (breaking changes, architecture shifts) require explicit approval from
majority of active contributors.
```

---

### 4. Steering Committee

**Structure:** Elected committee makes strategic decisions; maintainers handle day-to-day.

**Pros:**
- Separates strategy from tactics
- Formal structure for large projects
- Democratic representation

**Cons:**
- Heavy overhead
- Can become bureaucratic
- Requires elections

**Best For:**
- Large projects
- Foundation-governed projects
- Projects with multiple companies involved

**Example:**
```markdown
## Governance

**Steering Committee:** 5 members elected annually by contributors
- Sets project direction and roadmap
- Resolves major disputes
- Approves new maintainers
- Manages project assets

**Maintainers:** Handle day-to-day operations
- Review and merge PRs
- Triage issues
- Cut releases
- Enforce code of conduct
```

---

### 5. Company-Backed

**Structure:** Company employees make final decisions; community contributes.

**Pros:**
- Clear ownership
- Financial support
- Fast decisions
- Professional maintenance

**Cons:**
- Community may feel secondary
- Company priorities may conflict with community
- Risk of abandonment if company loses interest

**Best For:**
- Corporate open source projects
- Products with open source components
- Projects requiring significant resources

**Example:**
```markdown
## Governance

This project is maintained by Acme Corp. Final decisions rest with the Acme engineering
team. Community contributions are welcome and encouraged. Major changes are discussed
openly via GitHub issues before implementation.

For major feature proposals, open an issue with the "proposal" label for discussion.
```

---

## Choosing a Model

### Project Size

| Contributors | Recommended Model |
|--------------|-------------------|
| 1-2 | BDFL |
| 3-5 | Maintainer Team |
| 6-20 | Consensus-Based or Maintainer Team |
| 20+ | Steering Committee or Maintainer Team with sub-teams |

### Project Stage

**Early (0.x):** BDFL or small maintainer team
- Focus on building, not governance
- Flexibility to change direction
- Minimal process

**Growing (1.x-2.x):** Maintainer team
- Distribute responsibility
- Formalize contribution process
- Define roles

**Mature (3.x+):** Steering committee or formal governance
- Structured decision-making
- Clear succession plans
- Sub-teams for specialization

## Defining Roles

### Maintainer

**Responsibilities:**
- Review and merge pull requests
- Triage and respond to issues
- Cut releases
- Enforce code of conduct
- Guide new contributors

**Requirements:**
- Sustained contribution history
- Technical expertise
- Communication skills
- Time commitment

### Committer

**Responsibilities:**
- Write code and documentation
- Fix bugs
- Implement features
- Review others' contributions

**Requirements:**
- Several accepted contributions
- Understanding of codebase
- Follows contribution guidelines

### Contributor

**Responsibilities:**
- Submit pull requests
- Report bugs
- Help other users
- Improve documentation

**Requirements:**
- None - open to everyone

### Community Member

**Responsibilities:**
- Use the project
- Provide feedback
- Help others

**Requirements:**
- None - open to everyone

## Decision-Making Processes

### Lazy Consensus

Used for: Most day-to-day decisions

Process:
1. Propose change (issue, RFC, PR)
2. Wait for feedback period (3-7 days)
3. If no objections, proceed
4. If objections, address or modify proposal

Example:
```markdown
**Proposal:** Change default timeout from 30s to 60s

**Rationale:** 30s is too short for slow networks

**Impact:** Minor breaking change for users relying on default

**Feedback period:** Until 2025-12-15

If no objections by deadline, this will be implemented in next release.
```

### Explicit Approval

Used for: Major changes, breaking changes, new maintainers

Process:
1. Formal proposal
2. Discussion period
3. Vote (if required)
4. Implementation

Example:
```markdown
**RFC: Add Plugin System**

**Summary:** Proposal to add plugin architecture for extending functionality

**Motivation:** Users want to extend behavior without forking

**Design:** [Detailed design document]

**Breaking Changes:** None

**Approval Required:** 2+ maintainer approvals

**Vote:** React with 👍 (approve) or 👎 (object with reason)
```

### Voting

Used for: Major decisions when consensus can't be reached

Formats:
- **Simple majority:** >50% approve
- **Supermajority:** >66% approve
- **Consensus:** No objections (not unanimous)

Example:
```markdown
**Vote: Accept corporate sponsorship?**

Proposal: Accept $10k/year sponsorship from Acme Corp for hosting

Vote period: 2025-12-01 to 2025-12-08

Eligible voters: All maintainers (5 total)

Result: 4 approve, 1 abstain → **Accepted**
```

## Conflict Resolution

### Level 1: Discussion

Most conflicts resolved through:
- Open discussion in issues/PRs
- Bringing in different perspectives
- Finding compromise

### Level 2: Mediation

If discussion fails:
- Senior maintainer mediates
- Private conversation if needed
- Focus on project best interest

### Level 3: Escalation

If mediation fails:
- Steering committee decision (if exists)
- BDFL final call
- Vote among maintainers

### Level 4: Code of Conduct

For interpersonal conflicts:
- Follow code of conduct process
- Involve code of conduct committee
- May result in temporary or permanent ban

## Succession Planning

### Maintainer Burnout

Signs:
- Slow response to issues/PRs
- Declining contribution quality
- Expressing frustration
- Decreased engagement

Response:
- Check in privately
- Offer to reduce responsibilities
- Promote new maintainers
- Allow graceful exit

### Stepping Down

Process for maintainers leaving:
1. Announce intention to step down
2. Transition period (30-90 days)
3. Document knowledge and processes
4. Transfer critical responsibilities
5. Move to "emeritus" status

### Emergency Succession

If maintainer disappears:
1. Attempt to contact (email, other projects, social media)
2. Wait reasonable period (3-6 months)
3. Community discusses next steps
4. Fork or request repository transfer (if needed)
5. Continue project under new leadership

## Documenting Governance

Create `GOVERNANCE.md` file:

```markdown
# Governance

## Overview

This project is maintained by a team of volunteers following a maintainer team model.

## Roles

### Maintainers

Current maintainers:
- @alice (lead, releases)
- @bob (security)
- @carol (docs)

Responsibilities:
- Review PRs
- Triage issues
- Cut releases
- Guide contributors

### Contributors

Anyone who submits a PR or helps with issues.

## Decision Making

**Minor changes:** Any maintainer can approve
**Major changes:** Require 2+ maintainer approvals
**Breaking changes:** Require all maintainer approvals

Discussion period: Minimum 3 days for major changes

## Becoming a Maintainer

Requirements:
- 10+ accepted contributions
- 6+ months active participation
- Technical expertise in codebase
- Good communication skills

Process:
1. Existing maintainer nominates contributor
2. All maintainers vote
3. Requires unanimous approval
4. 90-day trial period

## Code of Conduct

We follow the [Contributor Covenant](CODE_OF_CONDUCT.md).

Reports handled by: @alice, @bob

## Changes to Governance

Changes to this document require all maintainer approval.
```

## Best Practices

1. **Start simple** - Don't over-govern small projects
2. **Document clearly** - Write down how decisions are made
3. **Be transparent** - Discuss decisions publicly
4. **Plan succession** - Don't be single point of failure
5. **Recognize contributors** - Celebrate contributions
6. **Resolve conflicts** - Don't let issues fester
7. **Evolve governance** - Adapt as project grows
8. **Be inclusive** - Welcome diverse contributors
9. **Communicate often** - Keep community informed
10. **Lead by example** - Follow your own rules

## Anti-Patterns

**Too much governance too soon:**
- 3-person project with 10-page governance doc
- Formal voting for minor decisions
- Requires committee approval for typo fixes

**Too little governance too late:**
- 50 contributors, no defined process
- Maintainer bottleneck causing delays
- Unclear who can approve PRs

**Governance theater:**
- Rules exist but aren't followed
- Democratic facade with BDFL reality
- Community feedback ignored

## Resources

- [Producing Open Source Software - Governance](https://producingoss.com/en/governments.html)
- [Kubernetes Governance](https://github.com/kubernetes/community/blob/master/governance.md)
- [Rust Governance](https://www.rust-lang.org/governance)
- [Python PEP 8016 - Steering Council](https://www.python.org/dev/peps/pep-8016/)
- [Apache Software Foundation Governance](https://www.apache.org/foundation/governance/)

---

Good governance grows with your project. Start simple, document decisions, and evolve as needed. The best governance is the one that helps your project succeed without getting in the way.
