# 6. Review DB Queries

**SQL injection is alive and well in AI-generated code.**

Use these prompts to audit database queries for injection vulnerabilities.

---

## Full Database Query Audit

```
Audit all database queries in my codebase for SQL injection:

[PASTE YOUR DATABASE CODE]

Database: [PostgreSQL / MySQL / MongoDB / Supabase / etc.]
ORM/Client: [Prisma / Drizzle / raw SQL / Mongoose / etc.]

Check every query for:
1. **String concatenation** - Is user input concatenated into queries?
2. **Template literals** - Are variables interpolated unsafely?
3. **Missing parameterization** - Are placeholders used for all user input?
4. **ORM misuse** - Are raw queries bypassing ORM protections?
5. **Dynamic table/column names** - Are these validated?
6. **LIKE clauses** - Is % properly escaped?
7. **ORDER BY injection** - Is sort direction validated?
8. **NoSQL injection** - For MongoDB, are operators ($gt, $where) blocked?

For each vulnerability:
- Show the vulnerable code
- Explain the attack
- Provide the secure fix
```

---

## Fix SQL Injection Vulnerabilities

```
Fix these SQL injection vulnerabilities:

[PASTE VULNERABLE CODE]

Convert each query to use:
1. Parameterized queries (preferred)
2. Prepared statements
3. ORM methods that auto-escape

Show before and after for each fix.
Also add input validation as defense in depth.
```

---

## Prisma Security Review

```
Review my Prisma queries for security issues:

[PASTE PRISMA CODE]

Check for:
1. **$queryRaw usage** - Is user input parameterized?
2. **$executeRaw usage** - Same concern
3. **Dynamic where clauses** - Built from user input safely?
4. **Relation traversal** - Could expose unauthorized data?
5. **Select/include** - Returning more fields than needed?

Show secure patterns for any issues found.
```

---

## Supabase Query Security

```
Review my Supabase queries for security:

[PASTE SUPABASE CLIENT CODE]

Check for:
1. **RLS bypass** - Am I accidentally using service role client-side?
2. **Filter injection** - Are .eq(), .like() etc. using validated input?
3. **RPC functions** - Are parameters validated in the function?
4. **Storage policies** - Can users access others' files?
5. **Realtime subscriptions** - Are they properly filtered?

Also verify RLS policies are enabled and correct.
```

---

## MongoDB/NoSQL Injection

```
Review my MongoDB queries for NoSQL injection:

[PASTE MONGODB CODE]

Check for:
1. **Operator injection** - Can user input include $gt, $ne, $where?
2. **Query object construction** - Is user input used as keys?
3. **$where clause** - Is JavaScript execution possible?
4. **Regex injection** - Are regex patterns from user input?
5. **Aggregation pipeline** - Are stages built from user input?

Show how to sanitize each vulnerable query.
```

---

## Input Validation for Queries

```
Add input validation before these database queries:

[PASTE QUERY CODE]

For each user input, add:
1. **Type validation** - Is it the expected type?
2. **Length limits** - Reasonable max length?
3. **Format validation** - Email, UUID, etc.?
4. **Allowlist validation** - For enums, sort fields, etc.
5. **Sanitization** - Remove/escape dangerous characters

Use [Zod / Yup / joi / etc.] for validation.
Show the validation schema and how to apply it.
```

---

## Common Vulnerable Patterns

### ❌ String concatenation (SQL Injection)
```javascript
// VULNERABLE - Never do this
const query = `SELECT * FROM users WHERE id = '${userId}'`;
const query = "SELECT * FROM users WHERE name = '" + name + "'";
```

### ✅ Parameterized query
```javascript
// SAFE - Always use parameters
const query = 'SELECT * FROM users WHERE id = $1';
await client.query(query, [userId]);

// Or with Prisma
await prisma.$queryRaw`SELECT * FROM users WHERE id = ${userId}`;
```

### ❌ Dynamic column names (Injection risk)
```javascript
// VULNERABLE
const query = `SELECT * FROM users ORDER BY ${sortColumn}`;
```

### ✅ Allowlist validation
```javascript
// SAFE - Validate against allowlist
const allowedColumns = ['name', 'email', 'created_at'];
if (!allowedColumns.includes(sortColumn)) {
  throw new Error('Invalid sort column');
}
const query = `SELECT * FROM users ORDER BY ${sortColumn}`;
```

### ❌ MongoDB operator injection
```javascript
// VULNERABLE - User could pass { $gt: "" }
const user = await User.findOne({ username: req.body.username });
```

### ✅ Sanitized MongoDB query
```javascript
// SAFE - Ensure it's a string
const username = String(req.body.username);
const user = await User.findOne({ username });

// Or use mongo-sanitize
import sanitize from 'mongo-sanitize';
const user = await User.findOne({ username: sanitize(req.body.username) });
```

---

## Testing for SQL Injection

```
Help me test my application for SQL injection:

Endpoint: [URL or code]
Input fields: [List fields that go to database]

Create test cases using:
1. Basic injection: ' OR '1'='1
2. Union-based: ' UNION SELECT * FROM users--
3. Time-based blind: ' AND SLEEP(5)--
4. Error-based: ' AND 1=CONVERT(int, @@version)--
5. Comment injection: admin'--

Show me:
1. Manual test payloads to try
2. How to use sqlmap for automated testing
3. What responses indicate vulnerability
4. How to test without breaking production
```

---

## ORM-Specific Security

### Prisma
```javascript
// Safe - Prisma auto-parameterizes
await prisma.user.findMany({
  where: { email: userInput }
});

// Careful with raw queries
await prisma.$queryRaw`SELECT * FROM users WHERE id = ${userId}`; // Safe
await prisma.$queryRawUnsafe(`SELECT * FROM users WHERE id = ${userId}`); // UNSAFE
```

### Drizzle
```javascript
// Safe - Uses prepared statements
await db.select().from(users).where(eq(users.email, userInput));

// Careful with sql template
import { sql } from 'drizzle-orm';
sql`SELECT * FROM users WHERE id = ${userId}`; // Safe - parameterized
```

### Sequelize
```javascript
// Safe - Parameterized
await User.findAll({ where: { email: userInput } });

// Careful with raw queries
await sequelize.query('SELECT * FROM users WHERE id = ?', {
  replacements: [userId] // Safe
});
```

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
