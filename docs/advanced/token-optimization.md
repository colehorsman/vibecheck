# Token Optimization

Save money. Get better results.

## TL;DR

- Use **10-15% of context** per request
- **TOON format** saves 30-60% on structured data
- **Specific references** beat full file pastes
- **Steering files** avoid repetition

---

## The 10-15% Rule

**Aim to use only 10-15% of the model's context window per request.**

This leaves room for:
- Model reasoning and chain-of-thought
- Tool responses and file contents
- Conversation history
- Error recovery and retries

### Why It Matters

**Stanford research findings:**
- Accuracy drops from 75% → 55% when relevant info is buried in 4K+ tokens
- Information at start and end of context is recalled better than middle
- Smaller, focused context = better results than large, comprehensive context

**Context engineering breakdown:**
| Factor | Impact on Output |
|--------|------------------|
| Model selection | ~15% |
| Prompt engineering | ~10% |
| Everything else (retrieval, memory, tools) | ~75% |

---

## Practical Techniques

### 1. Be Specific

```markdown
❌ Bad: "Here's my entire codebase, find the bug"
✅ Good: "In src/auth/login.ts, the validateToken function returns undefined when..."

❌ Bad: "Make it better"
✅ Good: "Reduce the cyclomatic complexity of the handleSubmit function"
```

### 2. Reference, Don't Paste

```markdown
❌ Bad: Pasting 500 lines of code
✅ Good: "Look at src/components/Dashboard.tsx, specifically the useEffect on line 45"
```

### 3. Use TOON Format for Data

TOON (Token-Oriented Object Notation) saves 30-60% on structured data.

**JSON (379 tokens):**
```json
{
  "logs": [
    {"id": 2001, "level": "error", "message": "Auth failed"},
    {"id": 2002, "level": "warn", "message": "Retry threshold"}
  ]
}
```

**TOON (150 tokens):**
```
logs[2]{id,level,message}:
  2001,error,Auth failed
  2002,warn,Retry threshold
```

→ [TOON Format Guide](toon-format.md)

### 4. Use Steering Files (Kiro)

Instead of repeating context every request:

```markdown
# .kiro/steering/project-context.md
---
inclusion: always
---

## Tech Stack
- Next.js 14, TypeScript, Supabase, Tailwind

## Patterns
- Server components by default
- Zod for validation
- Error boundaries for error handling
```

This context is automatically included without using your prompt tokens.

### 5. Break Large Tasks

```markdown
❌ Bad: "Build me a complete e-commerce site"

✅ Good (sequence):
1. "Create the product listing page"
2. "Add the shopping cart component"
3. "Implement checkout flow"
4. "Add payment integration"
```

---

## Token Savings by Technique

| Technique | Typical Savings |
|-----------|-----------------|
| TOON format for arrays | 30-60% |
| Specific file references | 40-80% |
| Steering files (Kiro) | Avoids repetition |
| Focused prompts | Better accuracy |
| Breaking large tasks | Prevents context overflow |

---

## Measuring Token Usage

### Claude Code

```bash
# Check token usage after a session
claude-code stats
```

### Cursor

Look at the token counter in the chat panel.

### Manual Estimation

- ~4 characters = 1 token (English)
- ~100 words = ~130 tokens
- Average code file = 500-2000 tokens

---

## Anti-Patterns

### ❌ Context Stuffing

Don't dump everything "just in case."

```markdown
Bad: "Here's my entire codebase, all my docs, and my life story. Now fix this bug."
```

### ❌ Vague Requests

Vague = AI asks for clarification = more tokens.

```markdown
Bad: "Make it work"
Good: "The login function should return a JWT token on success, null on failure"
```

### ❌ Repeating Context

Don't re-explain your tech stack every message.

```markdown
Bad: "Remember, we're using Next.js 14 with TypeScript and Supabase..."
Good: Use steering files or CLAUDE.md
```

---

## Quick Reference

| Situation | Optimization |
|-----------|--------------|
| Sending logs/data | Use TOON format |
| Referencing code | Point to file + line, don't paste |
| Project context | Use steering files |
| Large feature | Break into smaller tasks |
| Debugging | Include only relevant code |

---

*Less context. Better results. Lower costs.*
