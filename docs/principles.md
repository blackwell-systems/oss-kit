# Open Source Principles

Core principles for building trustworthy open source projects.

## Transparency

**Be open about decisions, changes, and limitations.**

- Document architectural decisions and tradeoffs
- Explain breaking changes clearly
- Acknowledge known issues and limitations
- Share roadmap and priorities openly

## Reliability

**Code should work as documented.**

- Write comprehensive tests
- Document prerequisites and dependencies
- Provide clear error messages
- Handle edge cases gracefully
- Test on target platforms

## Simplicity

**Minimize complexity where possible.**

- Favor simple solutions over clever ones
- Reduce dependencies
- Keep APIs small and focused
- Provide sensible defaults
- Document the "happy path" first

## Documentation

**Code without documentation is incomplete.**

- README should get users started in 5 minutes
- Every public API should have examples
- Breaking changes need migration guides
- Architecture decisions should be recorded
- Keep docs in sync with code

## Compatibility

**Respect semantic versioning.**

- Major version for breaking changes
- Minor version for new features
- Patch version for bug fixes
- Document deprecations with alternatives
- Support migration paths

## Security

**Take security seriously from day one.**

- Provide security contact information
- Never commit secrets or credentials
- Review dependencies regularly
- Respond to vulnerability reports promptly
- Document supported versions

## Community

**Contributors are partners, not free labor.**

- Respond to issues and PRs promptly
- Provide clear contribution guidelines
- Recognize contributions publicly
- Be respectful and inclusive
- Share credit generously

## Sustainability

**Plan for long-term maintenance.**

- Keep dependencies up to date
- Automate repetitive tasks
- Document project structure
- Plan for maintainer transitions
- Be honest about project status

## Pragmatism

**Perfect is the enemy of good.**

- Ship iteratively
- Gather real feedback
- Fix bugs before adding features
- Don't over-engineer
- Know when "good enough" is good enough

## Integrity

**Build trust through consistency.**

- Follow your own guidelines
- Admit and fix mistakes
- Don't make promises you can't keep
- Respect user privacy
- Be accountable

---

## Applying These Principles

### For New Projects

1. Start with README, LICENSE, and basic tests
2. Add CONTRIBUTING and SECURITY before first PR
3. Document decisions in CHANGELOG
4. Set up CI before v1.0
5. Add more governance as community grows

### For Existing Projects

1. Audit against checklist
2. Fix critical gaps (security, licensing)
3. Improve documentation gradually
4. Add automation incrementally
5. Engage with community feedback

### When in Doubt

- **Transparency**: Document it
- **Reliability**: Test it
- **Simplicity**: Remove it
- **Compatibility**: Version it
- **Security**: Review it

---

## Anti-Patterns to Avoid

- Copying code without attribution
- Ignoring security reports
- Breaking compatibility without warning
- Abandoning projects silently
- Demanding contributions
- Over-promising features
- Blocking contributors arbitrarily
- Accepting low-quality PRs to boost numbers

---

## Further Reading

- [Open Source Guide](https://opensource.guide/) - GitHub's comprehensive guide
- [The Cathedral and the Bazaar](http://www.catb.org/~esr/writings/cathedral-bazaar/) - Eric Raymond's classic essay
- [Producing Open Source Software](https://producingoss.com/) - Karl Fogel's book
- [Choose a License](https://choosealicense.com/) - License selection guide
- [Contributor Covenant](https://www.contributor-covenant.org/) - Code of conduct template

---

These principles are guidelines, not laws. Adapt them to your project's needs, but always prioritize transparency, reliability, and respect for users and contributors.
