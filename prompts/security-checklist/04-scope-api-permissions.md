# 4. Scope API Permissions

**Only request what you need. Least privilege prevents disasters.**

Use these prompts to audit and minimize API permissions.

---

## Audit API Permissions

```
Audit the API permissions in my project:

[PASTE YOUR CODE THAT USES APIS]

For each API/service I'm using, check:
1. **What permissions are requested?**
2. **What permissions are actually needed?**
3. **Are there overly broad scopes?**
4. **Can permissions be reduced?**

APIs to check:
- OpenAI / Anthropic / AI APIs
- Supabase / Firebase
- AWS services
- OAuth scopes (Google, GitHub, etc.)
- Database access levels
- Third-party APIs

For each finding:
- Current permission level
- Minimum required permission
- How to reduce scope
- Risk of current over-permission
```

---

## Supabase Row Level Security

```
Set up Row Level Security (RLS) for my Supabase tables:

Tables:
[DESCRIBE YOUR TABLES AND RELATIONSHIPS]

User model:
[DESCRIBE HOW USERS RELATE TO DATA]

I need RLS policies that:
1. Users can only read their own data
2. Users can only update their own data
3. Users can only delete their own data
4. Admins can access all data (if applicable)
5. Public data is readable by anyone (if applicable)

Generate:
1. SQL to enable RLS on each table
2. Policies for SELECT, INSERT, UPDATE, DELETE
3. How to test the policies work correctly
4. Common gotchas to avoid
```

---

## OAuth Scope Minimization

```
Review my OAuth implementation for scope minimization:

Provider: [Google / GitHub / Microsoft / etc.]
Current scopes requested: [LIST SCOPES]

My app needs to:
[DESCRIBE WHAT YOUR APP DOES WITH THE AUTH]

Check:
1. Are all requested scopes actually used?
2. Can any scopes be removed?
3. Are there more restrictive alternatives?
4. Am I requesting write access when read-only would work?

Provide the minimal scope list and explain each one.
```

---

## AWS IAM Least Privilege

```
Review this AWS IAM policy for least privilege:

[PASTE IAM POLICY JSON]

My application needs to:
[DESCRIBE WHAT YOUR APP DOES]

Check for:
1. **Wildcard resources** - Can we specify exact ARNs?
2. **Wildcard actions** - Can we list specific actions?
3. **Overly broad services** - Do we need all of S3 or just one bucket?
4. **Missing conditions** - Can we add IP, time, or MFA conditions?
5. **Unused permissions** - Are all actions actually used?

Provide the tightened policy with explanations.
```

---

## Database User Permissions

```
Set up least-privilege database users for my app:

Database: [PostgreSQL / MySQL / MongoDB]
Application needs:
- Read from: [tables/collections]
- Write to: [tables/collections]
- Never needs: [admin operations, schema changes, etc.]

Create:
1. Application user with minimal permissions
2. Migration user (for schema changes, used only in CI/CD)
3. Read-only user (for analytics/reporting)

Show the SQL/commands to create each user and grant permissions.
```

---

## API Key Scoping

```
Help me scope my API keys properly:

Service: [OpenAI / Stripe / Twilio / etc.]
Current setup: [Describe current key usage]

I need:
1. Separate keys for development vs production
2. Keys scoped to specific operations (if supported)
3. Key rotation strategy
4. Monitoring for unusual usage

For this service, what's the most restrictive key configuration that still works?
```

---

## Third-Party API Audit

```
Audit third-party API usage in my codebase:

[PASTE RELEVANT CODE OR LIST APIS USED]

For each API:
1. What data am I sending to it?
2. What permissions/scopes am I using?
3. Is there sensitive data being transmitted?
4. Can I reduce what I'm sending?
5. Is the API call necessary or can it be cached/batched?

Flag any APIs receiving more data than necessary.
```

---

## Permission Checklist by Service

### OpenAI / Anthropic
```
- [ ] Using project-specific API keys (not org-wide)
- [ ] Rate limits configured appropriately
- [ ] Usage alerts set up
- [ ] Not sending PII in prompts (or have DPA in place)
```

### Supabase
```
- [ ] RLS enabled on all tables
- [ ] Anon key only has public access
- [ ] Service role key only used server-side
- [ ] Storage buckets have proper policies
```

### AWS
```
- [ ] No wildcard (*) in resource ARNs
- [ ] Actions are specific (not s3:*)
- [ ] Conditions added where possible
- [ ] Separate roles for different functions
```

### OAuth
```
- [ ] Only requesting necessary scopes
- [ ] Using offline_access only if needed
- [ ] Not requesting write when read works
- [ ] Scopes match actual feature usage
```

---

## Quick Wins

### Before: Overly broad
```javascript
// Requesting all Google scopes
const scopes = [
  'https://www.googleapis.com/auth/drive',
  'https://www.googleapis.com/auth/calendar',
  'https://www.googleapis.com/auth/gmail.modify'
];
```

### After: Minimal scopes
```javascript
// Only what we actually use
const scopes = [
  'https://www.googleapis.com/auth/drive.file', // Only files we create
  'https://www.googleapis.com/auth/calendar.readonly' // Read-only
  // Removed gmail - we don't use it
];
```

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
