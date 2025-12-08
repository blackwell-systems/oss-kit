# Governance

This document describes the governance structure and decision-making process for Project Name.

## Overview

Project Name follows a **[BDFL / Maintainer Team / Consensus-Based / Committee]** governance model.

## Roles and Responsibilities

### Maintainers

**Current Maintainers:**
- [@alice](https://github.com/alice) - Lead Maintainer, Releases
- [@bob](https://github.com/bob) - Security, Infrastructure
- [@carol](https://github.com/carol) - Documentation, Community

**Responsibilities:**
- Review and merge pull requests
- Triage and respond to issues
- Cut releases
- Enforce code of conduct
- Guide contributors
- Make project decisions

**Requirements:**
- Sustained contribution history (10+ merged PRs)
- Technical expertise in codebase
- Good communication skills
- Time commitment (5+ hours per week)
- Demonstrates project values

### Committers

**Current Committers:**
- [@dave](https://github.com/dave)
- [@eve](https://github.com/eve)

**Responsibilities:**
- Write code and documentation
- Review pull requests
- Help with issue triage
- Support community members

**Requirements:**
- Regular contributions (5+ merged PRs)
- Understanding of codebase
- Follows contribution guidelines
- Active in community

### Contributors

Anyone who contributes to the project through:
- Code contributions
- Documentation improvements
- Bug reports
- Feature suggestions
- Community support

**No requirements** - all contributions welcome!

## Decision-Making Process

### Day-to-Day Decisions

**Examples:** Bug fixes, documentation updates, minor improvements

**Process:**
- Any maintainer can approve and merge
- Use judgment for risk assessment
- Consult other maintainers if unsure

### Minor Changes

**Examples:** New features, API additions, dependency updates

**Process:**
1. Propose change via issue or RFC
2. Discussion period (minimum 3 days)
3. Require 2 maintainer approvals
4. Implement and merge

### Major Changes

**Examples:** Breaking changes, architectural shifts, major refactors

**Process:**
1. Create detailed RFC (Request for Comments)
2. Community discussion period (minimum 7 days)
3. Require all maintainer approvals
4. Create migration plan if needed
5. Implement and merge

### Urgent Changes

**Examples:** Security fixes, critical bugs

**Process:**
- Single maintainer can approve
- Inform other maintainers ASAP
- Post-merge review if needed

### Project Direction

**Examples:** Roadmap changes, governance changes, major strategic decisions

**Process:**
1. Proposal posted publicly
2. Extended discussion period (14+ days)
3. Require consensus (all maintainers agree)
4. If no consensus, lead maintainer decides
5. Document decision publicly

## Voting

### When Required

- New maintainer nominations
- Governance changes
- Controversial decisions without consensus

### Eligible Voters

- All current maintainers
- Voting weight: 1 vote per maintainer

### Voting Process

1. **Proposal Posted**: Clear description of decision
2. **Discussion Period**: Minimum 7 days
3. **Voting Period**: 7 days
4. **Vote Format**: Comment with +1 (approve), 0 (abstain), -1 (object with reason)
5. **Quorum**: 66% of maintainers must vote
6. **Threshold**: Simple majority (>50%) to pass

### Example Vote

```markdown
**Vote: Accept Corporate Sponsorship**

Proposal: Accept $10,000/year sponsorship from Acme Corp for infrastructure costs.

Discussion period: 2025-01-01 to 2025-01-07
Voting period: 2025-01-08 to 2025-01-14

Eligible voters: @alice, @bob, @carol (3 total)

Votes:
- @alice: +1
- @bob: +1
- @carol: 0 (abstain)

Result: 2/2 approve (100%) - **PASSED**
```

## Becoming a Maintainer

### Process

1. **Nomination**: Current maintainer nominates contributor
2. **Evaluation**: Review contribution history and qualifications
3. **Vote**: All maintainers vote (requires unanimous approval)
4. **Trial Period**: 90-day probationary period
5. **Confirmation**: Permanent status after successful trial

### Requirements

- **Technical**:
  - 10+ merged pull requests
  - 6+ months active participation
  - Deep understanding of codebase
  - High-quality contributions

- **Community**:
  - Helpful and respectful communication
  - Regular engagement (issues, PRs, discussions)
  - Mentors other contributors
  - Follows code of conduct

- **Commitment**:
  - Available 5+ hours per week
  - Responsive to issues/PRs
  - Participates in project planning

### Responsibilities

New maintainers receive:
- Write access to repository
- Access to private maintainer discussions
- Decision-making authority
- Listed in GOVERNANCE.md and README.md

## Removing a Maintainer

### Voluntary Resignation

Maintainers may step down:
- By notifying other maintainers
- Transition period recommended (30-90 days)
- Move to "emeritus" status
- Recognition in documentation

### Involuntary Removal

A maintainer may be removed for:
- Violations of code of conduct
- Sustained inactivity (6+ months without communication)
- Breach of trust or security
- Repeated poor judgment

**Process:**
1. Private discussion among maintainers
2. Attempt to resolve issues
3. Vote (requires 75% approval)
4. Inform removed maintainer
5. Update documentation

## Emeritus Maintainers

Former maintainers who:
- Voluntarily stepped down in good standing
- Recognized for past contributions
- May return to active status if desired

**Current Emeritus:**
- [@frank](https://github.com/frank) - Original creator, retired 2024

## Conflict Resolution

### Level 1: Discussion

- Discuss disagreement openly in issue/PR
- Seek to understand different perspectives
- Find compromise or middle ground

### Level 2: Mediation

If discussion doesn't resolve:
- Senior maintainer facilitates discussion
- Private conversation if interpersonal
- Focus on project best interest

### Level 3: Vote

If mediation fails:
- Call for formal vote
- Follow voting process (see above)
- Majority decision is final

### Level 4: Code of Conduct

For interpersonal conflicts:
- Report to conduct@example.com
- Code of Conduct committee investigates
- May result in temporary or permanent ban

## Communication

### Public Channels

- **GitHub Issues**: Bug reports, feature requests
- **GitHub Discussions**: Questions, ideas, general discussion
- **Discord/Slack**: Real-time chat
- **Mailing List**: Announcements

### Private Channels

- **Maintainer Email**: maintainers@example.com
- **Security Email**: security@example.com
- **Code of Conduct**: conduct@example.com

### Meetings

- **Maintainer Sync**: Weekly (private)
- **Community Call**: Monthly (public)
- **Planning Session**: Quarterly (public)

Meeting notes posted to GitHub Discussions.

## Code of Conduct

All participants must follow the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md).

**Enforcement:**
- Violations reported to conduct@example.com
- Handled by code of conduct committee: @alice, @bob
- Consequences range from warning to permanent ban

## Intellectual Property

### Copyright

- Individual contributors retain copyright
- Contributions licensed under project license (see [LICENSE](LICENSE))
- No contributor agreement required

### Trademarks

- Project name and logos owned by [Organization/Maintainers]
- Usage guidelines: [link to trademark policy]

## Modifications to Governance

Changes to this document require:
- Proposal with rationale
- 14-day discussion period
- Unanimous maintainer approval
- Or 75% maintainer vote if unanimous not possible

## Historical Decisions

Record of major governance decisions:

### 2025-01-15: Adopted maintainer team model
- **Context**: Project growing beyond single maintainer
- **Decision**: Transition from BDFL to maintainer team
- **Vote**: Unanimous approval

### 2024-12-01: Accepted sponsorship
- **Context**: Need funding for infrastructure
- **Decision**: Accept corporate sponsorship with transparency
- **Vote**: 2-0 with 1 abstention

## Resources

- [Producing Open Source Software - Governance](https://producingoss.com/en/governments.html)
- [Kubernetes Governance](https://github.com/kubernetes/community/blob/master/governance.md)
- [Rust Governance](https://www.rust-lang.org/governance)
- [CNCF Governance](https://contribute.cncf.io/resources/governance/)

## Questions?

For questions about governance:
- Open a [discussion](https://github.com/yourorg/yourproject/discussions)
- Email maintainers: maintainers@example.com
- Attend monthly community call

---

**Last Updated:** YYYY-MM-DD

**Next Review:** YYYY-MM-DD (Annual review)

This governance structure is designed to be lightweight enough for efficient operation while providing clear processes for decision-making and conflict resolution.
