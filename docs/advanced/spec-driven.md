# Spec-Driven Development

From vibe code to viable code.

## TL;DR

- **Specs** = structured requirements before AI writes code
- **EARS format** = unambiguous requirement syntax
- **Kiro** = AWS IDE built for spec-driven development
- **Result** = better code, better docs, fewer hallucinations

---

## Why Spec-Driven?

> "Spec-driven development is about making the AI's reasoning visible and reviewable before it writes code."
> — Marc Brooker, AWS VP

### Benefits

1. **Reduces hallucinations** — AI has clear constraints
2. **Enables review** — Catch issues at requirements stage (cheaper than code review)
3. **Creates documentation** — Specs become living docs
4. **Improves consistency** — Same format across projects
5. **Supports iteration** — Easy to modify and regenerate

---

## The Spec Flow

```
Idea → Requirements → Design → Tasks → Code → Tests
```

Each step is documented and reviewable before moving forward.

### 1. Requirements

What the feature should do. User stories, acceptance criteria.

### 2. Design

How it will work. Architecture, data flow, components.

### 3. Tasks

Specific implementation steps. Small, focused chunks.

### 4. Code

Generated from tasks with full context.

### 5. Tests

Validation that requirements are met.

---

## EARS Format

**Easy Approach to Requirements Syntax** — unambiguous requirements.

| Pattern | Template | Example |
|---------|----------|---------|
| **Ubiquitous** | The system shall [action] | The system shall encrypt all data at rest |
| **Event-driven** | When [trigger], the system shall [action] | When user clicks login, the system shall validate credentials |
| **State-driven** | While [state], the system shall [action] | While offline, the system shall queue requests |
| **Optional** | Where [condition], the system shall [action] | Where user is admin, the system shall show settings |
| **Unwanted** | If [condition], the system shall [action] | If session expires, the system shall redirect to login |

### Example EARS Requirement

```markdown
## Requirement: Session Management

**Event-driven:** When a user successfully authenticates, the system shall create a JWT token valid for 24 hours.

**State-driven:** While a valid session exists, the system shall allow access to protected routes.

**Unwanted behavior:** If the token expires, the system shall return 401 and redirect to login.
```

---

## Kiro Workflow

### 1. Create a Spec

```bash
# In Kiro
Cmd+Shift+P → "Kiro: New Spec"
```

Describe your feature:
```
Build user authentication with email/password login, 
session management, and password reset via email.
```

### 2. Review Generated Requirements

Kiro generates EARS-format requirements. Review and edit:

```markdown
# Feature: User Authentication

## Requirements

**Event-driven:** When a user submits valid credentials, the system shall create a session and redirect to dashboard.

**Event-driven:** When a user requests password reset, the system shall send a reset link to their email.

**Unwanted:** If credentials are invalid, the system shall display an error without revealing which field is wrong.

## Acceptance Criteria
- [ ] Login form validates email format
- [ ] Password must be 8+ characters
- [ ] Failed attempts rate-limited to 5 per minute
- [ ] Reset link expires after 1 hour
```

### 3. Approve Design

Kiro proposes architecture:

```markdown
## Design

### Components
- AuthService: Handles authentication logic
- UserRepository: Database operations
- EmailService: Password reset emails

### Data Flow
1. User submits credentials
2. AuthService validates against UserRepository
3. JWT token generated on success
4. Token stored in httpOnly cookie
```

### 4. Execute Tasks

Kiro breaks into tasks and implements:

```markdown
## Tasks
- [x] Create User model
- [x] Implement AuthService
- [ ] Add login endpoint
- [ ] Add signup endpoint
- [ ] Implement password reset
```

---

## Steering Files

Persistent context that applies across all interactions.

### Project Context

```markdown
# .kiro/steering/project-context.md
---
inclusion: always
---

## Tech Stack
- Framework: Next.js 14
- Database: Supabase
- Styling: Tailwind CSS
- Auth: Supabase Auth

## Architecture
- App Router for routing
- Server components by default
- API routes for backend logic
```

### Code Style

```markdown
# .kiro/steering/code-style.md
---
inclusion: always
---

## TypeScript
- Strict mode enabled
- Explicit return types on functions
- Zod for runtime validation

## React
- Functional components only
- Custom hooks for shared logic
- Error boundaries for error handling
```

### Security

```markdown
# .kiro/steering/security.md
---
inclusion: always
---

## Rules
- Never hardcode secrets
- Use environment variables
- Validate all user inputs
- Use parameterized queries
- Sanitize output to prevent XSS
```

### Inclusion Modes

```yaml
---
inclusion: always      # Always included (default)
---

---
inclusion: fileMatch   # Only when matching files are in context
fileMatchPattern: "*.tsx"
---

---
inclusion: manual      # Only when explicitly referenced with #
---
```

---

## Spec Checklist

Before approving a spec:

- [ ] Requirements use EARS format
- [ ] Acceptance criteria are testable
- [ ] Design includes data flow
- [ ] Tasks are small (< 1 hour each)
- [ ] Edge cases documented
- [ ] Security requirements explicit

---

## The "Vibe to Viable" Workflow

From AWS re:Invent 2025:

```
1. VIBE: Quick prototype with minimal spec
   └── "Build a todo app with Supabase"

2. VALIDATE: Test with real users
   └── Identify missing requirements

3. SPECIFY: Write proper specs for gaps
   └── EARS format, acceptance criteria

4. VIABLE: Production-ready implementation
   └── Full specs, tests, documentation
```

---

## Resources

- [Kiro Documentation](https://kiro.dev/docs)
- [kiro.directory](https://kiro.directory) — Community best practices
- [Real Python Podcast #277](https://realpython.com/podcasts/rpp/277/) — Marc Brooker on spec-driven development

---

*Structure your intent. Let AI execute.*
