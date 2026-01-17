# 5. Use Secrets Scanner

**Automate secret detection. Humans miss things.**

Use these prompts to set up and run secrets scanning.

---

## Set Up Gitleaks

```
Set up gitleaks as a secrets scanner for my project:

Project type: [Node.js / Python / etc.]
Package manager: [npm / yarn / pip / etc.]
CI/CD: [GitHub Actions / GitLab CI / etc.]

I need:
1. Installation instructions
2. Configuration file (.gitleaks.toml) with rules for:
   - AWS credentials (AKIA*, aws_secret)
   - OpenAI/Anthropic API keys (sk-*)
   - Database URLs with passwords
   - JWT secrets
   - Private keys
   - Generic high-entropy strings
3. Pre-commit hook setup
4. CI/CD integration
5. How to handle false positives
6. How to scan existing git history

Make it block commits and PRs if secrets are found.
```

---

## Gitleaks Configuration

```
Create a custom .gitleaks.toml configuration:

My project uses these services:
[LIST YOUR SERVICES - e.g., OpenAI, Supabase, AWS, Stripe]

I need rules to detect:
1. API keys for each service (with their specific patterns)
2. Database connection strings
3. Private keys and certificates
4. OAuth client secrets
5. Webhook secrets
6. Generic passwords in config files

Also add allowlist entries for:
- Test files with fake credentials
- Documentation examples
- .env.example files

Show me the complete .gitleaks.toml file.
```

---

## GitHub Actions Secret Scanning

```
Set up secret scanning in GitHub Actions:

Repository: [public / private]
Branch protection: [yes / no]

Create a workflow that:
1. Runs gitleaks on every push and PR
2. Scans the full git history on schedule (weekly)
3. Fails the build if secrets are found
4. Posts results as PR comments
5. Sends alerts for critical findings

Also enable:
- GitHub's built-in secret scanning (if available)
- Push protection to block secrets before they're pushed

Show me the complete workflow YAML.
```

---

## Scan Existing Repository

```
I need to scan my existing repository for secrets that may have been committed:

Repository size: [small / medium / large]
Git history: [short / long - years of commits]

Give me:
1. Command to scan entire git history with gitleaks
2. How to interpret the results
3. How to prioritize findings (critical vs low risk)
4. Steps to remediate each type of secret found:
   - Remove from history (BFG or git filter-branch)
   - Rotate the credential
   - Update .gitignore
5. How to verify the secret is fully removed

Also: Should I assume all found secrets are compromised?
```

---

## Pre-Commit Hook Setup

```
Set up a pre-commit hook that scans for secrets before every commit:

Project uses: [npm / yarn / pip / etc.]
Hook manager preference: [husky / lefthook / pre-commit / none]

The hook should:
1. Run gitleaks on staged files only (fast)
2. Block the commit if secrets are found
3. Show clear error messages with file and line
4. Allow bypass for emergencies (with warning)
5. Not slow down normal commits significantly

Show me the exact setup steps and configuration files.
```

---

## Multiple Scanner Setup

```
Set up multiple secret scanners for defense in depth:

I want to use:
1. gitleaks - for git history and pre-commit
2. truffleHog - for entropy-based detection
3. GitHub secret scanning - for known patterns
4. detect-secrets (Yelp) - for baseline comparison

Show me how to:
1. Install and configure each
2. Run them in CI/CD
3. Deduplicate findings
4. Handle different output formats
5. Create a unified report

Which scanner catches what the others miss?
```

---

## Handle False Positives

```
I'm getting false positives from my secrets scanner:

Scanner: [gitleaks / truffleHog / etc.]
False positive examples:
[PASTE EXAMPLES OF FALSE POSITIVES]

Help me:
1. Add allowlist entries for these specific cases
2. Create rules that are more precise
3. Exclude test files and documentation
4. Keep the scanner effective while reducing noise

Show me the configuration changes needed.
```

---

## Quick Setup Commands

### Gitleaks
```bash
# Install (macOS)
brew install gitleaks

# Install (npm - for CI)
npm install -g gitleaks

# Scan current directory
gitleaks detect --source . --verbose

# Scan git history
gitleaks detect --source . --verbose --log-opts="--all"

# Generate report
gitleaks detect --source . --report-format json --report-path gitleaks-report.json
```

### TruffleHog
```bash
# Install
pip install truffleHog

# Scan repository
trufflehog git file://. --only-verified

# Scan with entropy detection
trufflehog git file://. --entropy
```

### detect-secrets (Yelp)
```bash
# Install
pip install detect-secrets

# Create baseline
detect-secrets scan > .secrets.baseline

# Audit baseline
detect-secrets audit .secrets.baseline

# Scan for new secrets
detect-secrets scan --baseline .secrets.baseline
```

---

## CI/CD Integration

### GitHub Actions
```yaml
name: Secret Scanning
on: [push, pull_request]

jobs:
  gitleaks:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### GitLab CI
```yaml
gitleaks:
  image: zricethezav/gitleaks:latest
  script:
    - gitleaks detect --source . --verbose
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
```

---

## What Each Scanner Catches

| Scanner | Strengths | Weaknesses |
|---------|-----------|------------|
| **gitleaks** | Fast, configurable, git-aware | Needs good rules |
| **truffleHog** | Entropy detection, verified secrets | Slower, more false positives |
| **detect-secrets** | Baseline comparison, plugins | Setup complexity |
| **GitHub native** | Zero config, push protection | Limited to known patterns |
| **AWS Security Agent** | Full app context, pen testing, OWASP/MITRE | AWS-focused, preview |

**Recommendation:** Use gitleaks for pre-commit + CI, enable GitHub native scanning, run truffleHog periodically for deep scans.

---

## AWS Security Agent (Preview)

AWS Security Agent is a frontier AI agent that proactively secures your applications throughout the development lifecycle. It understands your entire application architecture, code, and security requirements.

### What It Does
- **Design Review:** Assesses architecture against security best practices before code is written
- **Code Scanning:** Continuous vulnerability scanning with full application context
- **Penetration Testing:** On-demand pen testing without scheduling
- **Threat Modeling:** Generates threat models based on your specific application

### Setup
```bash
# AWS Security Agent is in preview - request access at:
# https://aws.amazon.com/security-agent

# Once enabled, it integrates with your AWS environment automatically
```

### Use Cases
```
Ask AWS Security Agent to:
1. Review my application architecture for security flaws
2. Scan my repository for OWASP Top 10 vulnerabilities
3. Generate a threat model for my application
4. Run penetration tests against my staging environment
5. Map findings to MITRE ATT&CK framework
```

---

## OWASP Top 10 Scanning

The OWASP Top 10 represents the most critical web application security risks. Use these prompts to scan for them.

### Scan for OWASP Top 10

```
Scan my codebase for OWASP Top 10 vulnerabilities:

Project type: [Node.js / Python / etc.]
Framework: [Express / FastAPI / Next.js / etc.]

Check for:
1. A01:2021 - Broken Access Control
   - Missing authorization checks
   - IDOR vulnerabilities
   - Path traversal

2. A02:2021 - Cryptographic Failures
   - Weak encryption
   - Hardcoded secrets
   - Insecure data transmission

3. A03:2021 - Injection
   - SQL injection
   - NoSQL injection
   - Command injection
   - XSS

4. A04:2021 - Insecure Design
   - Missing rate limiting
   - No input validation
   - Trust boundary violations

5. A05:2021 - Security Misconfiguration
   - Debug mode in production
   - Default credentials
   - Unnecessary features enabled

6. A06:2021 - Vulnerable Components
   - Outdated dependencies
   - Known CVEs
   - Unmaintained packages

7. A07:2021 - Authentication Failures
   - Weak passwords allowed
   - Missing MFA
   - Session fixation

8. A08:2021 - Software and Data Integrity
   - Missing integrity checks
   - Insecure deserialization
   - CI/CD vulnerabilities

9. A09:2021 - Security Logging Failures
   - Missing audit logs
   - Sensitive data in logs
   - No alerting

10. A10:2021 - SSRF
    - Unvalidated URLs
    - Internal service access

For each finding, show:
- File and line number
- Severity (Critical/High/Medium/Low)
- How to fix it
- Example secure code
```

### OWASP Quick Scan Commands

```bash
# Semgrep - OWASP rules
semgrep --config "p/owasp-top-ten" .

# Bandit (Python)
bandit -r . -f json -o bandit-report.json

# npm audit (Node.js)
npm audit --json > npm-audit.json

# Snyk
snyk test --json > snyk-report.json

# OWASP Dependency Check
dependency-check --scan . --format JSON --out dependency-check-report.json
```

---

## MITRE ATT&CK Mapping

Map your security findings to the MITRE ATT&CK framework for better threat understanding.

### Generate Threat Model

```
Generate a threat model for my application using MITRE ATT&CK:

Application type: [Web app / API / Mobile / etc.]
Architecture: [Describe your architecture]
Data sensitivity: [Public / Internal / Confidential / Restricted]

Map potential attacks to:
1. Initial Access techniques
2. Execution techniques
3. Persistence techniques
4. Privilege Escalation techniques
5. Defense Evasion techniques
6. Credential Access techniques
7. Discovery techniques
8. Lateral Movement techniques
9. Collection techniques
10. Exfiltration techniques

For each relevant technique:
- Show the ATT&CK ID (e.g., T1190)
- Explain how it applies to my app
- Recommend mitigations
- Suggest detection methods
```

### Map Vulnerabilities to MITRE

```
I found these vulnerabilities in my scan:
[PASTE YOUR SCAN RESULTS]

Map each vulnerability to:
1. MITRE ATT&CK technique ID
2. Tactic category
3. Real-world attack scenarios
4. Detection opportunities
5. Recommended mitigations

Create a prioritized remediation plan based on:
- Likelihood of exploitation
- Impact if exploited
- Ease of remediation
```

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
