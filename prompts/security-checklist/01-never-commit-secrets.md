# 1. Never Commit Secrets

**The #1 cause of security breaches in vibe-coded projects.**

Use these prompts to ensure secrets never make it into your repository.

---

## Setup: Create Secure Environment Files

```
I'm starting a new project. Help me set up secure secret management:

1. Create a .env.example file with placeholder values for:
   - Database connection string
   - API keys (OpenAI, Supabase, etc.)
   - Auth secrets (JWT secret, session secret)
   - Any third-party service credentials

2. Create a comprehensive .gitignore that excludes:
   - All .env files (.env, .env.local, .env.*.local)
   - Private keys (*.pem, *.key)
   - IDE settings
   - OS files (.DS_Store, Thumbs.db)
   - Node modules, Python venv, etc.

3. Add a pre-commit hook using husky that:
   - Runs gitleaks to scan for secrets
   - Blocks commits if secrets are detected

Show me the exact files to create and commands to run.
```

---

## Scan Existing Code for Secrets

```
Scan this codebase for accidentally committed secrets:

[PASTE YOUR CODE OR FILE STRUCTURE]

Look for:
1. Hardcoded API keys (patterns like sk-*, pk_*, api_key=)
2. Database connection strings with passwords
3. JWT secrets or session secrets in code
4. AWS credentials (AKIA*, aws_secret_access_key)
5. Private keys or certificates
6. OAuth client secrets
7. Webhook secrets
8. Any string that looks like a password or token

For each finding:
- Show the exact line and file
- Explain the risk
- Show how to move it to .env
- Provide the fix

Also check if .gitignore properly excludes .env files.
```

---

## Install Pre-Commit Secret Scanner

```
Set up gitleaks as a pre-commit hook to prevent secrets from ever being committed.

My project uses: [npm/yarn/pnpm] and [git]

Give me:
1. Installation commands
2. Configuration file (.gitleaks.toml) with rules for:
   - API keys (OpenAI, Anthropic, AWS, GCP, Azure)
   - Database URLs with passwords
   - Private keys
   - JWT secrets
   - Generic high-entropy strings
3. Pre-commit hook setup (using husky or lefthook)
4. How to run a one-time scan of existing commits
5. How to handle false positives

Make it so commits are blocked if secrets are detected.
```

---

## Fix: Secret Already Committed

```
I accidentally committed a secret to git. Help me fix this:

Secret type: [API key / database password / private key / etc.]
File: [filename]
How many commits ago: [number or "not sure"]

I need:
1. How to remove the secret from git history (git filter-branch or BFG)
2. How to rotate/regenerate the compromised credential
3. How to properly add it to .env going forward
4. How to force-push the cleaned history
5. What to tell collaborators who have the old history

Also: Should I consider this credential compromised even if the repo is private?
```

---

## Environment Variable Best Practices

```
Review my environment variable setup:

.env.example:
[PASTE YOUR .env.example]

.gitignore:
[PASTE YOUR .gitignore]

Code that uses env vars:
[PASTE RELEVANT CODE]

Check for:
1. Are all secrets in .env (not hardcoded anywhere)?
2. Is .env in .gitignore?
3. Does .env.example have safe placeholder values (not real secrets)?
4. Are env vars validated at startup (fail fast if missing)?
5. Are there any secrets that shouldn't be in .env.example?
6. Is there a README section explaining how to set up .env?

Provide fixes for any issues.
```

---

## Quick Commands

### Install gitleaks (macOS)
```bash
brew install gitleaks
```

### Scan current directory
```bash
gitleaks detect --source . --verbose
```

### Scan git history
```bash
gitleaks detect --source . --verbose --log-opts="--all"
```

### Add to package.json scripts
```json
{
  "scripts": {
    "secrets:scan": "gitleaks detect --source . --verbose",
    "secrets:scan:history": "gitleaks detect --source . --verbose --log-opts='--all'"
  }
}
```

---

## Common Patterns to Avoid

❌ **Don't do this:**
```javascript
const apiKey = "sk-1234567890abcdef";
const dbUrl = "postgres://user:password@host:5432/db";
```

✅ **Do this instead:**
```javascript
const apiKey = process.env.OPENAI_API_KEY;
const dbUrl = process.env.DATABASE_URL;

// Validate at startup
if (!apiKey) throw new Error("OPENAI_API_KEY is required");
```

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
