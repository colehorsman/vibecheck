# Security Checklist Prompts

**The 7-point checklist that prevents 80% of vibe coding disasters.**

Each prompt gives you everything you need to secure that aspect of your project.

---

## The Checklist

| # | Item | Prompt | Risk Level |
|---|------|--------|------------|
| 1 | [Never commit secrets](01-never-commit-secrets.md) | Setup .env, gitleaks, pre-commit hooks | 🔴 Critical |
| 2 | [Review auth code](02-review-auth-code.md) | Audit AI-generated authentication | 🔴 Critical |
| 3 | [Check .gitignore](03-check-gitignore.md) | Ensure nothing sensitive is tracked | 🟠 High |
| 4 | [Scope API permissions](04-scope-api-permissions.md) | Least privilege for all APIs | 🟠 High |
| 5 | [Use secrets scanner](05-use-secrets-scanner.md) | Automate secret detection | 🟠 High |
| 6 | [Review DB queries](06-review-db-queries.md) | Prevent SQL/NoSQL injection | 🔴 Critical |
| 7 | [Test error handling](07-test-error-handling.md) | Don't leak info in errors | 🟡 Medium |

---

## Quick Start

### Before Your First Commit
1. **[01-never-commit-secrets.md](01-never-commit-secrets.md)** — Set up .env and .gitignore
2. **[03-check-gitignore.md](03-check-gitignore.md)** — Verify nothing sensitive is tracked
3. **[05-use-secrets-scanner.md](05-use-secrets-scanner.md)** — Install pre-commit hook

### Before Going Public
4. **[02-review-auth-code.md](02-review-auth-code.md)** — Audit all authentication
5. **[06-review-db-queries.md](06-review-db-queries.md)** — Check for injection
6. **[04-scope-api-permissions.md](04-scope-api-permissions.md)** — Minimize access
7. **[07-test-error-handling.md](07-test-error-handling.md)** — Hide stack traces

---

## How to Use

Each prompt file contains:
- **Multiple prompt templates** for different scenarios
- **Quick commands** you can copy-paste
- **Common mistakes** to avoid
- **Before/after examples** showing the fix

### Example Workflow

```bash
# 1. Copy the prompt you need
open vibecheck/prompts/security-checklist/01-never-commit-secrets.md

# 2. Paste into your AI tool (Claude, ChatGPT, Cursor, etc.)

# 3. Fill in the [PLACEHOLDERS] with your code

# 4. Apply the fixes

# 5. Check it off your list ✅
```

---

## The 80% Rule

These 7 items prevent 80% of security issues in vibe-coded projects:

- **Secrets in git** — #1 cause of breaches
- **Weak auth** — AI often skips or simplifies
- **SQL injection** — Still the most common vulnerability
- **Info leakage** — Stack traces help attackers

The other 20% requires deeper security review, but this checklist gets you most of the way there.

---

## Integration with Slides

These prompts are linked from the [VibeCheck slide deck](../../../vibecheck-slides/). When presenting:

1. Show the security checklist slide
2. Click an item to open the prompt
3. Walk through the prompt with the audience
4. They can use it immediately on their projects

---

## Contributing

Found a better prompt? Missing a common scenario? PRs welcome.

---

*Part of the [VibeCheck](../../README.md) project.*
