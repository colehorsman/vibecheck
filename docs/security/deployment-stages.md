# Deployment Security Stages

A passing security score is required before deploying infrastructure.

## TL;DR

| Stage | Tools | What It Catches |
|-------|-------|-----------------|
| **Pre-Commit** | git-secrets, gitleaks | Secrets in code |
| **Pre-Deploy** | Checkov, tfsec, Semgrep | IaC misconfigs, code vulns |
| **Deploy Gate** | CI/CD pipeline | Blocks deploy if scans fail |
| **Post-Deploy** | GuardDuty, Security Hub | Runtime threats |

---

## Stage 1: Pre-Commit

Catch secrets before they enter git history.

### Setup

```bash
# Install git-secrets
brew install git-secrets

# Initialize in repo
git secrets --install
git secrets --register-aws

# Install gitleaks
brew install gitleaks
```

### Pre-commit Hook

Create `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.18.0
    hooks:
      - id: gitleaks

  - repo: https://github.com/awslabs/git-secrets
    rev: master
    hooks:
      - id: git-secrets
```

Install:
```bash
pip install pre-commit
pre-commit install
```

---

## Stage 2: Pre-Deploy Scanning

Scan infrastructure and code before deployment.

### IaC Security Tools

| Tool | Best For | Install |
|------|----------|---------|
| **Checkov** | Comprehensive IaC | `pip install checkov` |
| **tfsec** | Terraform-specific | `brew install tfsec` |
| **Terrascan** | Multi-framework | `brew install terrascan` |
| **Semgrep** | Code + IaC | `pip install semgrep` |

### Usage

```bash
# Checkov - scan Terraform
checkov -d ./terraform

# tfsec - Terraform security
tfsec ./terraform

# Semgrep - code vulnerabilities
semgrep --config auto .

# Trivy - containers + IaC
trivy fs .
```

### Minimum Passing Scores

| Tool | Threshold |
|------|-----------|
| Checkov | 0 HIGH, 0 CRITICAL |
| tfsec | 0 HIGH, 0 CRITICAL |
| Semgrep | 0 ERROR |

---

## Stage 3: CI/CD Deploy Gate

Block deployment if security scans fail.

### GitHub Actions Example

```yaml
# .github/workflows/security.yml
name: Security Scan

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run gitleaks
        uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Run Checkov
        uses: bridgecrewio/checkov-action@master
        with:
          directory: .
          soft_fail: false

      - name: Run Semgrep
        uses: returntocorp/semgrep-action@v1
        with:
          config: auto
```

### Vercel/Netlify

Add to build command:
```bash
npm run security-scan && npm run build
```

In `package.json`:
```json
{
  "scripts": {
    "security-scan": "gitleaks detect && semgrep --config auto .",
    "build": "next build"
  }
}
```

---

## Stage 4: Post-Deploy Monitoring

Runtime security monitoring.

### AWS

- **GuardDuty** - Threat detection
- **Security Hub** - Centralized findings
- **CloudTrail** - API audit logs
- **Config** - Resource compliance

### Application

- **Sentry** - Error tracking (check for sensitive data in errors)
- **Datadog** - APM with security monitoring
- **LogRocket** - Session replay (be careful with PII)

---

## Quick Setup Script

```bash
#!/bin/bash
# setup-security.sh

# Install tools
brew install git-secrets gitleaks tfsec
pip install checkov semgrep pre-commit

# Initialize git-secrets
git secrets --install
git secrets --register-aws

# Create pre-commit config
cat > .pre-commit-config.yaml << 'EOF'
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.18.0
    hooks:
      - id: gitleaks
EOF

# Install pre-commit hooks
pre-commit install

echo "Security tools installed!"
```

---

## Checklist by Stage

### Pre-Commit
- [ ] git-secrets installed
- [ ] gitleaks installed
- [ ] Pre-commit hooks configured
- [ ] Team trained on secret handling

### Pre-Deploy
- [ ] Checkov passing
- [ ] tfsec passing (if using Terraform)
- [ ] Semgrep passing
- [ ] No HIGH/CRITICAL findings

### Deploy Gate
- [ ] CI/CD pipeline includes security scans
- [ ] Deployment blocked on failures
- [ ] Alerts configured for failures

### Post-Deploy
- [ ] GuardDuty enabled (AWS)
- [ ] Security Hub enabled (AWS)
- [ ] Error tracking configured
- [ ] Audit logging enabled

---

## Resources

- [Checkov Documentation](https://www.checkov.io/1.Welcome/Quick%20Start.html)
- [tfsec Documentation](https://aquasecurity.github.io/tfsec/)
- [Semgrep Rules](https://semgrep.dev/explore)
- [GitHub Security Features](https://docs.github.com/en/code-security)

---

*Security gates aren't blockers. They're guardrails.*
