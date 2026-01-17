# Security Checklist

The 7 things that prevent 80% of vibe coding disasters.

## TL;DR

Print this. Put it next to your monitor.

- [ ] **1. Never commit secrets**
- [ ] **2. Review auth code**
- [ ] **3. Check .gitignore**
- [ ] **4. Scope API permissions**
- [ ] **5. Use secrets scanner**
- [ ] **6. Review DB queries**
- [ ] **7. Test error handling**

---

## The Checklist (Detailed)

### 1. Never Commit Secrets

**The problem:** AI often hardcodes API keys, passwords, and tokens directly in code.

**The fix:**
```bash
# Create .env file
touch .env

# Add secrets there
SUPABASE_URL=your-url
SUPABASE_KEY=your-key
OPENAI_API_KEY=sk-...

# Add to .gitignore
echo ".env" >> .gitignore
echo ".env.local" >> .gitignore
echo ".env*.local" >> .gitignore
```

**In code:**
```javascript
// ❌ Bad
const apiKey = "sk-1234567890abcdef";

// ✅ Good
const apiKey = process.env.OPENAI_API_KEY;
```

---

### 2. Review Authentication Code

**The problem:** AI often skips auth entirely or implements it poorly.

**What to check:**
- [ ] Login actually validates credentials
- [ ] Sessions expire appropriately
- [ ] Password reset is secure
- [ ] Protected routes check auth
- [ ] Logout invalidates session

**Red flags:**
```javascript
// ❌ Bad - No actual validation
if (password) {
  return { success: true };
}

// ✅ Good - Proper validation
const user = await db.users.findByEmail(email);
const valid = await bcrypt.compare(password, user.passwordHash);
if (!valid) throw new Error("Invalid credentials");
```

---

### 3. Check Your .gitignore

**The problem:** AI doesn't always know what to exclude.

**Essential .gitignore entries:**
```gitignore
# Environment
.env
.env.local
.env*.local

# Dependencies
node_modules/
.pnpm-store/

# Build
.next/
dist/
build/

# IDE
.idea/
.vscode/
*.swp

# OS
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*

# Secrets
*.pem
*.key
```

---

### 4. Scope API Permissions

**The problem:** AI often requests more permissions than needed.

**The fix:**
- Only request permissions you actually use
- Use read-only access when possible
- Prefer scoped tokens over admin tokens

**Example (Supabase):**
```javascript
// ❌ Bad - Using service role key in client
const supabase = createClient(url, SERVICE_ROLE_KEY);

// ✅ Good - Using anon key with RLS
const supabase = createClient(url, ANON_KEY);
```

---

### 5. Use a Secrets Scanner

**The problem:** Secrets slip through despite best intentions.

**Tools:**
```bash
# git-secrets (AWS)
brew install git-secrets
git secrets --install
git secrets --register-aws

# gitleaks
brew install gitleaks
gitleaks detect

# truffleHog
pip install truffleHog
trufflehog git file://./
```

**GitHub built-in:**
- Enable "Secret scanning" in repo settings
- Enable "Push protection" to block commits with secrets

---

### 6. Review Database Queries

**The problem:** SQL injection is alive and well in AI-generated code.

**What to check:**
```javascript
// ❌ Bad - String concatenation
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ Good - Parameterized query
const query = `SELECT * FROM users WHERE id = $1`;
const result = await db.query(query, [userId]);

// ✅ Good - ORM/Query builder
const user = await db.users.findUnique({ where: { id: userId } });
```

---

### 7. Test Error Handling

**The problem:** AI often exposes stack traces and internal details in errors.

**What to check:**
```javascript
// ❌ Bad - Exposes internals
catch (error) {
  return res.status(500).json({ error: error.stack });
}

// ✅ Good - Generic message
catch (error) {
  console.error(error); // Log internally
  return res.status(500).json({ error: "Something went wrong" });
}
```

**Test these scenarios:**
- [ ] Invalid input
- [ ] Missing auth
- [ ] Database errors
- [ ] Network failures
- [ ] Rate limiting

---

## Quick Scan Commands

Run these before deploying:

```bash
# Check for hardcoded secrets
grep -r "sk-" --include="*.js" --include="*.ts" .
grep -r "password" --include="*.js" --include="*.ts" .

# Check .gitignore exists and has .env
cat .gitignore | grep ".env"

# Run gitleaks
gitleaks detect --source . --verbose

# Check for console.log with sensitive data
grep -r "console.log" --include="*.js" --include="*.ts" . | grep -i "password\|token\|key\|secret"
```

---

## Pre-Deploy Checklist

Before every deployment:

- [ ] Secrets in `.env`, not in code
- [ ] `.env` in `.gitignore`
- [ ] Secrets scanner passed
- [ ] Auth code reviewed manually
- [ ] DB queries use parameters
- [ ] Error messages are generic
- [ ] API permissions are scoped
- [ ] HTTPS enabled
- [ ] Rate limiting configured

---

## Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [GitHub Secret Scanning](https://docs.github.com/en/code-security/secret-scanning)
- [git-secrets](https://github.com/awslabs/git-secrets)
- [gitleaks](https://github.com/gitleaks/gitleaks)

---

*Security isn't optional. It's the foundation.*
