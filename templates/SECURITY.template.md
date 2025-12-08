# Security Policy

## Supported Versions

We release security updates for the following versions:

| Version | Supported |
| ------- | --------- |
| 1.x.x   | Yes       |
| 0.9.x   | Yes       |
| < 0.9   | No        |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

### Where to Report

Report security vulnerabilities to:

**Email:** security@example.com

**PGP Key:** [Download PGP Key](https://example.com/pgp-key.asc) (Fingerprint: `XXXX XXXX XXXX XXXX`)

Alternatively, you can use GitHub's private vulnerability reporting:

1. Go to the [Security tab](https://github.com/yourorg/yourproject/security)
2. Click "Report a vulnerability"
3. Fill out the form with details

### What to Include

Please include the following information:

- **Type of vulnerability** (e.g., SQL injection, XSS, authentication bypass)
- **Affected version(s)**
- **Step-by-step reproduction instructions**
- **Proof of concept** (if available)
- **Impact assessment** (what an attacker could achieve)
- **Suggested fix** (if you have one)

### Response Timeline

- **Acknowledgment:** Within 48 hours
- **Initial assessment:** Within 5 business days
- **Status update:** Weekly until resolved
- **Fix release:** Depends on severity (see below)

### Severity Levels

We use the CVSS v3.1 scoring system:

| Severity | CVSS Score | Response Time |
|----------|------------|---------------|
| Critical | 9.0-10.0   | 24-48 hours   |
| High     | 7.0-8.9    | 7 days        |
| Medium   | 4.0-6.9    | 30 days       |
| Low      | 0.1-3.9    | 90 days       |

### Disclosure Policy

We follow responsible disclosure:

1. **Report received** - Acknowledged within 48 hours
2. **Validation** - We confirm the vulnerability
3. **Fix development** - We develop and test a fix
4. **Security patch release** - Fix released in new version
5. **Public disclosure** - 90 days after fix release or coordinated disclosure

### Security Advisories

After a fix is released, we will:

1. Publish a GitHub Security Advisory
2. Update CHANGELOG.md with security fix details
3. Credit the reporter (unless they wish to remain anonymous)
4. Notify users via:
   - GitHub releases
   - Security mailing list (if subscribed)
   - Project blog/website

### Embargo Period

We appreciate advance notice before public disclosure. We typically request:

- **Critical vulnerabilities:** 30-90 days
- **High vulnerabilities:** 60-90 days
- **Medium/Low vulnerabilities:** 90 days

If you need to disclose earlier, please let us know your timeline.

### Bug Bounty

We do not currently offer a bug bounty program. However:

- We will credit you in release notes
- We will add you to our security acknowledgments
- We deeply appreciate your contribution to project security

### Security Best Practices

When using this project:

#### Secure Configuration

```yaml
# Don't commit secrets to git
api_key: ${API_KEY}  # Use environment variables

# Use strong authentication
auth:
  method: oauth2
  min_password_length: 12

# Enable security features
security:
  tls_enabled: true
  require_auth: true
```

#### Environment Variables

```bash
# Don't hardcode secrets
export API_KEY="your-secret-key"
export DB_PASSWORD="your-db-password"

# Use secret management
# - Cloud providers (AWS Secrets Manager, Azure Key Vault)
# - Password managers (1Password, Bitwarden)
# - Environment-specific configs
```

#### Dependencies

```bash
# Keep dependencies updated
go get -u ./...
go mod tidy

# Check for vulnerabilities
go list -json -m all | nancy sleuth

# Or use GitHub Dependabot (enabled by default)
```

### Known Security Considerations

#### 1. Authentication

This project requires you to:
- Configure authentication before production use
- Use strong passwords/tokens
- Rotate credentials regularly

#### 2. Network Security

This project:
- Supports TLS/HTTPS (enable in production)
- Does not include firewall rules (configure separately)
- Binds to 0.0.0.0 by default (restrict in production)

#### 3. Input Validation

This project:
- Validates user input where possible
- May not cover all edge cases
- Should not be exposed directly to untrusted input

### Security-Related Configuration

```yaml
# Example secure configuration
server:
  tls:
    enabled: true
    cert_file: /path/to/cert.pem
    key_file: /path/to/key.pem

  cors:
    allowed_origins:
      - https://trusted-domain.com

  rate_limiting:
    enabled: true
    requests_per_minute: 100

auth:
  required: true
  session_timeout: 3600
  max_login_attempts: 5

logging:
  level: info
  sanitize_secrets: true
```

### Third-Party Dependencies

We monitor security advisories for our dependencies:

- GitHub Dependabot alerts enabled
- Regular dependency updates
- Security scanning in CI/CD

See [go.mod](go.mod) for full dependency list.

### Security Contacts

**Primary:** security@example.com
**Backup:** maintainer@example.com

**GPG Key:**
Fingerprint: `XXXX XXXX XXXX XXXX XXXX XXXX XXXX XXXX XXXX XXXX`
Download: [security-key.asc](https://example.com/security-key.asc)

### Security Acknowledgments

We thank the following individuals for responsibly disclosing security issues:

- **2025-01**: [@username](https://github.com/username) - SQL injection in query parser
- **2024-12**: [@username](https://github.com/username) - Authentication bypass

(Add your organization's Hall of Fame here)

### Additional Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [CWE Top 25](https://cwe.mitre.org/top25/)
- [Go Security Best Practices](https://github.com/guardrailsio/awesome-golang-security)

### Frequently Asked Questions

**Q: Do you have a vulnerability disclosure program?**
A: Yes, please email security@example.com with details.

**Q: Can I publicly disclose a vulnerability I found?**
A: Please give us 90 days to fix it first, or coordinate with us on disclosure timing.

**Q: Do you offer rewards for security reports?**
A: We don't have a formal bug bounty, but we recognize contributors publicly.

**Q: What if I find a vulnerability in a dependency?**
A: Report it to the dependency's maintainers and notify us so we can track the fix.

**Q: How do I know if a release contains security fixes?**
A: Check the CHANGELOG.md for entries marked "Security" or GitHub Security Advisories.

---

**Last Updated:** YYYY-MM-DD
**Version:** 1.0

Thank you for helping keep Project Name and our users secure!
