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

**Recommendation:** Use gitleaks for pre-commit + CI, enable GitHub native scanning, run truffleHog periodically for deep scans.

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
