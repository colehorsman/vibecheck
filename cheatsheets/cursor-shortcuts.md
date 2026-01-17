# Cursor Shortcuts Cheatsheet

Print this. Keep it handy.

## Essential Shortcuts

| Action | Mac | Windows |
|--------|-----|---------|
| **AI Chat** | `Cmd+L` | `Ctrl+L` |
| **Inline Edit** | `Cmd+K` | `Ctrl+K` |
| **Accept Suggestion** | `Tab` | `Tab` |
| **Reject Suggestion** | `Esc` | `Esc` |
| **Terminal AI** | `Cmd+K` (in terminal) | `Ctrl+K` |

## Chat Commands

| Command | What It Does |
|---------|--------------|
| `@codebase` | Search entire codebase |
| `@file` | Reference specific file |
| `@folder` | Reference folder |
| `@docs` | Search documentation |
| `@web` | Search the web |

## Inline Edit (Cmd+K)

1. Select code (or place cursor)
2. Press `Cmd+K`
3. Describe what you want
4. Press `Enter`
5. Review and accept/reject

**Example prompts:**
- "Add error handling"
- "Convert to TypeScript"
- "Add comments"
- "Refactor to use async/await"

## Chat (Cmd+L)

**Good prompts:**
```
Explain this function
Why is this failing?
How do I add authentication?
Write tests for this component
```

**With context:**
```
@file:src/auth.ts explain the login flow
@codebase where is the user model defined?
```

## Terminal (Cmd+K in terminal)

**Example prompts:**
```
Install supabase
Run tests
Start dev server
Create new component
```

## Pro Tips

1. **Be specific** - "Add error handling for network failures" > "Add error handling"
2. **Use @file** - Reference specific files for context
3. **Iterate** - Ask follow-up questions
4. **Review** - Always check generated code

## .cursorrules

Create `.cursorrules` in project root:

```markdown
# Project: My App

## Tech Stack
- Next.js 14
- TypeScript
- Supabase

## Rules
- Use server components by default
- Always add error handling
- Use Zod for validation
```

---

*Cmd+L to chat. Cmd+K to edit. Tab to accept.*
