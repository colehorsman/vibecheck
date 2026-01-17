# Claude Code Commands Cheatsheet

Print this. Keep it handy.

## Installation

```bash
npm install -g @anthropic-ai/claude-code
claude-code auth
```

## Basic Usage

```bash
# Start interactive session
claude-code

# Run specific task
claude-code "Add user authentication"

# With file context
claude-code "Fix the bug in auth.ts"
```

## In-Session Commands

| Command | What It Does |
|---------|--------------|
| `/help` | Show all commands |
| `/clear` | Clear conversation |
| `/compact` | Summarize and continue |
| `/cost` | Show token usage |
| `/doctor` | Check configuration |

## CLAUDE.md

Create `CLAUDE.md` in project root:

```markdown
# Project: My App

## Tech Stack
- Next.js 14
- Supabase
- TypeScript

## Commands
- npm run dev - Start server
- npm run test - Run tests

## Structure
/app - Pages
/components - React components
/lib - Utilities

## Rules
- Use TypeScript
- Add error handling
- Never hardcode secrets
```

## MCP Integration

Configure in `~/.claude/mcp.json`:

```json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["-y", "@supabase/mcp-server"]
    }
  }
}
```

## Good Prompts

```
# Specific
"In src/auth/login.ts, fix the token validation on line 45"

# With context
"Add a new API endpoint for user profiles, following the pattern in /api/users"

# Multi-step
"Refactor the auth module:
1. Extract validation logic
2. Add error handling
3. Add tests"
```

## Pro Tips

1. **Use CLAUDE.md** - Saves tokens, provides context
2. **Be specific** - File names, line numbers, exact behavior
3. **Review changes** - Always check before accepting
4. **Use /compact** - When context gets long

## Permission Modes

| Mode | What It Does |
|------|--------------|
| `--dangerously-skip-permissions` | No confirmations (use carefully) |
| Default | Asks before file changes |

---

*claude-code to start. /help for commands.*
