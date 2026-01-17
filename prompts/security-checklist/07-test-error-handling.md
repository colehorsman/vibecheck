# 7. Test Error Handling

**AI exposes stack traces. Check what your errors reveal.**

Use these prompts to audit error handling and prevent information leakage.

---

## Full Error Handling Audit

```
Audit error handling in my application:

[PASTE YOUR CODE - especially API routes, error handlers, catch blocks]

Framework: [Next.js / Express / FastAPI / etc.]
Environment: [development / production]

Check for:
1. **Stack traces exposed** - Are full stack traces sent to clients?
2. **Database errors leaked** - Do DB errors reveal schema/queries?
3. **File paths exposed** - Are server paths visible in errors?
4. **Sensitive data in errors** - User data, tokens, credentials?
5. **Verbose error messages** - Do they help attackers?
6. **Missing error boundaries** - Unhandled exceptions crashing the app?
7. **Inconsistent error formats** - Different shapes for different errors?
8. **Missing logging** - Are errors logged server-side?

For each issue:
- Show the problematic code
- Explain what information leaks
- Provide the secure fix
```

---

## Create Safe Error Handler

```
Create a production-safe error handling system:

Framework: [Next.js / Express / FastAPI / etc.]
Logging: [console / Winston / Pino / etc.]

I need:
1. **Global error handler** that:
   - Catches all unhandled errors
   - Logs full details server-side
   - Returns safe, generic messages to clients
   - Includes error ID for support correlation

2. **Error response format**:
   - Consistent JSON structure
   - User-friendly messages
   - No sensitive details
   - Different detail levels for dev vs prod

3. **Specific handlers** for:
   - Validation errors (400)
   - Authentication errors (401)
   - Authorization errors (403)
   - Not found errors (404)
   - Rate limit errors (429)
   - Server errors (500)

Show me the complete implementation.
```

---

## Test Error Responses

```
Help me test what my error responses reveal:

Application URL: [localhost:3000 or describe endpoints]
Framework: [Next.js / Express / etc.]

Create test cases that trigger:
1. **Invalid input** - Malformed JSON, wrong types
2. **Missing resources** - Non-existent IDs
3. **Auth failures** - Invalid tokens, missing auth
4. **Database errors** - Invalid queries, connection issues
5. **File errors** - Missing files, permission issues
6. **Rate limits** - Too many requests
7. **Unhandled exceptions** - Divide by zero, null reference

For each test:
- Show the request to make
- What response to expect (safe)
- What response indicates a problem (leaking info)
- How to fix if it's leaking
```

---

## Next.js Error Handling

```
Set up production-safe error handling for Next.js:

App Router: [yes / no]
API Routes: [yes / no]

I need:
1. **Global error boundary** (error.tsx)
2. **Not found page** (not-found.tsx)
3. **API route error handling**
4. **Server action error handling**
5. **Middleware error handling**

Each should:
- Log full error details server-side
- Show user-friendly message client-side
- Never expose stack traces in production
- Include error tracking (Sentry/etc.) integration

Show me the complete setup.
```

---

## Express Error Handling

```
Set up production-safe error handling for Express:

[PASTE CURRENT ERROR HANDLING CODE IF ANY]

I need:
1. **Custom error classes** for different error types
2. **Async error wrapper** for route handlers
3. **Global error middleware** that:
   - Logs full details
   - Returns safe responses
   - Handles different error types differently
4. **404 handler** for unknown routes
5. **Uncaught exception handler**

Show me the complete implementation with examples.
```

---

## Sanitize Error Messages

```
Sanitize these error messages for production:

[PASTE ERROR MESSAGES YOUR APP CURRENTLY RETURNS]

For each message:
1. Identify what sensitive info it reveals
2. Create a safe alternative message
3. Show what to log server-side vs return to client

Categories to handle:
- Database errors → "Unable to process request"
- Auth errors → "Invalid credentials" (not "user not found")
- Validation errors → Specific field errors (safe)
- Server errors → "Something went wrong"
```

---

## Error Logging Setup

```
Set up secure error logging:

Logger: [Winston / Pino / console / etc.]
Error tracking: [Sentry / Bugsnag / none]
Environment: [Node.js / Python / etc.]

I need:
1. **Structured logging** with:
   - Timestamp
   - Error ID (for correlation)
   - Error type/code
   - Stack trace (server logs only)
   - Request context (sanitized)
   - User ID (if authenticated)

2. **Log levels**:
   - Error: Unexpected failures
   - Warn: Handled but notable
   - Info: Normal operations
   - Debug: Development only

3. **Sensitive data filtering**:
   - Never log passwords
   - Never log full tokens
   - Mask PII in logs
   - Redact request bodies with secrets

Show me the configuration and usage examples.
```

---

## Common Mistakes

### ❌ Exposing stack traces
```javascript
app.use((err, req, res, next) => {
  res.status(500).json({
    error: err.message,
    stack: err.stack // NEVER DO THIS IN PRODUCTION
  });
});
```

### ✅ Safe error response
```javascript
app.use((err, req, res, next) => {
  // Log full error server-side
  console.error('Error:', {
    id: req.id,
    message: err.message,
    stack: err.stack,
    path: req.path
  });
  
  // Return safe response to client
  res.status(500).json({
    error: 'Something went wrong',
    errorId: req.id // For support correlation
  });
});
```

### ❌ Database error leakage
```javascript
catch (err) {
  // Reveals table names, column names, query structure
  res.status(500).json({ error: err.message });
}
```

### ✅ Generic database error
```javascript
catch (err) {
  console.error('Database error:', err);
  res.status(500).json({ error: 'Unable to process request' });
}
```

### ❌ Auth error reveals user existence
```javascript
if (!user) return res.status(404).json({ error: 'User not found' });
if (!validPassword) return res.status(401).json({ error: 'Wrong password' });
```

### ✅ Generic auth error
```javascript
if (!user || !validPassword) {
  return res.status(401).json({ error: 'Invalid credentials' });
}
```

---

## Error Response Checklist

```
Review my error responses against this checklist:

[ ] No stack traces in production responses
[ ] No database error details exposed
[ ] No file paths revealed
[ ] No internal IP addresses shown
[ ] No query parameters with secrets logged
[ ] No user passwords in any logs
[ ] Auth errors don't reveal user existence
[ ] Validation errors are specific but safe
[ ] 500 errors are generic to users
[ ] All errors logged server-side with context
[ ] Error IDs allow support correlation
[ ] Different error detail in dev vs prod
```

---

## Quick Test Commands

```bash
# Test with invalid JSON
curl -X POST http://localhost:3000/api/endpoint \
  -H "Content-Type: application/json" \
  -d "not valid json"

# Test with missing auth
curl http://localhost:3000/api/protected

# Test with invalid ID
curl http://localhost:3000/api/users/invalid-uuid

# Test rate limiting
for i in {1..100}; do curl http://localhost:3000/api/endpoint; done
```

---

*This prompt is part of the [VibeCheck Security Checklist](../README.md).*
