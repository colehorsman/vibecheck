# 3. Check .gitignore

**AI doesn't always know what to exclude. Verify your .gitignore is complete.**

Use these prompts to audit and fix your .gitignore.

---

## Generate Complete .gitignore

```
Generate a comprehensive .gitignore for my project:

Project type: [Next.js / React / Python / Node.js / etc.]
Package manager: [npm / yarn / pnpm / pip / etc.]
Database: [Supabase / Firebase / Postgres / MongoDB / etc.]
Deployment: [Vercel / AWS / Railway / etc.]
IDE: [VS Code / Cursor / WebStorm / etc.]
OS: [macOS / Windows / Linux]

Include entries for:
1. Environment files (.env, .env.local, .env.*.local)
2. Secrets and keys (*.pem, *.key, *.p12)
3. Dependencies (node_modules, venv, __pycache__)
4. Build outputs (.next, dist, build, .vercel)
5. IDE settings (.vscode, .idea, *.swp)
6. OS files (.DS_Store, Thumbs.db)
7. Logs (*.log, npm-debug.log)
8. Test coverage (coverage/, .nyc_output)
9. Cache directories (.cache, .turbo)
10. Local database files (*.sqlite, *.db)

Add comments explaining each section.
```

---

## Audit Existing .gitignore

```
Audit this .gitignore for completeness:

[PASTE YOUR .gitignore]

My project uses:
- Framework: [Next.js / etc.]
- Language: [TypeScript / Python / etc.]
- Database: [Supabase / etc.]

Check for:
1. **Missing .env patterns** - All variations covered?
2. **Missing secrets** - Private keys, certificates?
3. **Missing dependencies** - node_modules, venv?
4. **Missing build outputs** - .next, dist, build?
5. **Missing IDE files** - .vscode, .idea?
6. **Missing OS files** - .DS_Store, Thumbs.db?
7. **Missing logs** - *.log files?
8. **Missing cache** - .cache, .turbo?
9. **Overly broad patterns** - Accidentally ignoring important files?
10. **Missing local data** - SQLite files, local DBs?

Provide the additions needed.
```

---

## Check What's Being Tracked

```
I want to verify my .gitignore is working correctly.

Here's my .gitignore:
[PASTE .gitignore]

Here's my project structure:
[PASTE output of: find . -type f -not -path './.git/*' | head -100]

Check:
1. Are any .env files being tracked that shouldn't be?
2. Are any secret files (*.pem, *.key) being tracked?
3. Are node_modules or other dependencies being tracked?
4. Are build outputs being tracked?
5. Are any IDE or OS files being tracked?

Tell me what's wrong and how to fix it (including removing from git history if needed).
```

---

## Fix: File Already Tracked

```
I have files that are in .gitignore but were already committed. Help me fix this:

Files that need to be untracked:
[LIST FILES - e.g., .env, node_modules/, .DS_Store]

Give me:
1. Commands to remove from git tracking (but keep locally)
2. How to verify they're no longer tracked
3. Whether I need to clean git history (for secrets)
4. What to tell collaborators

Use git rm --cached for files that should stay local.
```

---

## .gitignore for Specific Stacks

### Next.js + Supabase + Vercel
```
Generate a .gitignore for:
- Next.js 14 with App Router
- Supabase for database and auth
- Vercel for deployment
- TypeScript
- Tailwind CSS
- VS Code as IDE
- macOS development

Include everything needed for this stack, with comments.
```

### Python FastAPI + PostgreSQL
```
Generate a .gitignore for:
- Python 3.11 with FastAPI
- PostgreSQL database
- Poetry for dependencies
- Docker for local development
- VS Code as IDE
- macOS/Linux development

Include everything needed for this stack, with comments.
```

---

## Quick .gitignore Template

```gitignore
# ===== SECRETS =====
# Environment variables
.env
.env.local
.env.*.local
.env.development
.env.production

# Private keys and certificates
*.pem
*.key
*.p12
*.pfx
*.crt

# ===== DEPENDENCIES =====
node_modules/
.pnpm-store/
venv/
.venv/
__pycache__/
*.pyc

# ===== BUILD =====
.next/
.nuxt/
dist/
build/
out/
.vercel/
.netlify/

# ===== IDE =====
.vscode/
.idea/
*.swp
*.swo
*~

# ===== OS =====
.DS_Store
.DS_Store?
Thumbs.db
ehthumbs.db

# ===== LOGS =====
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# ===== CACHE =====
.cache/
.turbo/
.eslintcache
.stylelintcache

# ===== TEST =====
coverage/
.nyc_output/

# ===== LOCAL DATA =====
*.sqlite
*.sqlite3
*.db
data/
```

---

## Verify .gitignore is Working

```bash
# Check if a file is ignored
git check-ignore -v .env

# List all ignored files
git status --ignored

# See what would be committed
git status

# Remove file from tracking (keep locally)
git rm --cached .env
git rm --cached -r node_modules/

# After updating .gitignore, clear cache
git rm -r --cached .
git add .
git commit -m "Update .gitignore"
```

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
