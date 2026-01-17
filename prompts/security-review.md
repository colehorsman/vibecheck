# Security Review Prompt

Use this to review code for security vulnerabilities.

---

## The Prompt

```
Review this code for security vulnerabilities:

[PASTE CODE HERE]

Check for:
1. Hardcoded secrets or credentials
2. SQL injection vulnerabilities
3. XSS (Cross-Site Scripting) risks
4. Authentication/authorization issues
5. Insecure data handling
6. Missing input validation
7. Exposed error messages
8. Insecure dependencies

For each issue found:
- Describe the vulnerability
- Explain the risk (what could happen)
- Provide the fix with code example

If no issues found, confirm the code looks secure and explain why.
```

---

## Quick Security Check

```
Quick security scan of this code:

[PASTE CODE HERE]

Flag any:
- Hardcoded secrets
- Missing auth checks
- Unvalidated inputs
- SQL/NoSQL injection risks
- XSS vulnerabilities

Just list issues with line numbers. I'll fix them.
```

---

## Auth Code Review

```
Review this authentication code:

[PASTE AUTH CODE HERE]

Check for:
1. Password handling (hashing, storage)
2. Session management
3. Token security (JWT issues)
4. Rate limiting
5. Account enumeration
6. Password reset flow security
7. CSRF protection

Provide specific fixes for any issues.
```

---

## API Endpoint Review

```
Review this API endpoint for security:

[PASTE ENDPOINT CODE HERE]

Check for:
1. Authentication required?
2. Authorization (who can access?)
3. Input validation
4. Rate limiting
5. Error handling (no stack traces)
6. CORS configuration
7. Request size limits

Provide fixes with code examples.
```

---

## Environment Variables Check

```
Review my environment setup:

.env.example:
[PASTE .env.example]

.gitignore:
[PASTE .gitignore]

Check:
1. Are all secrets in .env (not hardcoded)?
2. Is .env in .gitignore?
3. Are there any secrets that shouldn't be in .env.example?
4. Any missing entries in .gitignore?
```

---

## Pre-Deploy Security Checklist

```
I'm about to deploy this app. Run through this security checklist:

1. [ ] No hardcoded secrets in code
2. [ ] .env files in .gitignore
3. [ ] All user inputs validated
4. [ ] SQL queries parameterized
5. [ ] Auth on all protected routes
6. [ ] Error messages don't expose internals
7. [ ] HTTPS enforced
8. [ ] Dependencies up to date
9. [ ] Rate limiting on auth endpoints
10. [ ] CORS properly configured

Here's my codebase structure:
[PASTE STRUCTURE OR KEY FILES]

Flag any issues before I deploy.
```

---

## Tips

- Review auth code manually, even after AI review
- Run a secrets scanner (git-secrets, gitleaks)
- Check dependencies with `npm audit` or `pip audit`
- Test error handling with invalid inputs
