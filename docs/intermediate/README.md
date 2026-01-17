# Intermediate Guide

You know some code. Time to go faster.

## TL;DR

1. Install **Cursor** (or Windsurf)
2. Set up your project with proper configs
3. Use AI for the boring stuff, review the important stuff
4. Deploy with security checks

---

## Requirements

Before you start:

- [ ] Basic HTML/CSS/JS knowledge
- [ ] VS Code experience (or similar IDE)
- [ ] GitHub account
- [ ] Node.js installed (for most projects)
- [ ] 1-2 hours for setup + first project

→ [Full Requirements](requirements.md)

---

## Recommended Tools

| Tool | Cost | Best For |
|------|------|----------|
| **Cursor** | $20/mo | Best overall AI IDE |
| **Windsurf** | Free | Cursor alternative |
| **GitHub Copilot** | $10/mo | Best value, inline suggestions |
| **Supabase** | Free tier | Backend in minutes |

**Start with Cursor.** It's the game changer for intermediate developers.

---

## Cursor Setup

### 1. Install Cursor

Download from [cursor.com](https://cursor.com). It's a VS Code fork, so everything transfers.

### 2. Configure .cursorrules

Create `.cursorrules` in your project root:

```markdown
# Project: [Your Project Name]

## Tech Stack
- Framework: Next.js 14
- Database: Supabase
- Styling: Tailwind CSS
- Language: TypeScript

## Code Style
- Use TypeScript strict mode
- Prefer server components
- Use Zod for validation
- Keep functions small and focused

## Security
- Never hardcode secrets
- Use environment variables
- Validate all user inputs
- Use parameterized queries

## When generating code
- Add comments for complex logic
- Include error handling
- Follow existing patterns in the codebase
```

### 3. Set Up .env

```bash
# .env.local (never commit this)
SUPABASE_URL=your-url
SUPABASE_ANON_KEY=your-key
```

Add to `.gitignore`:
```
.env
.env.local
.env*.local
```

---

## Workflow: AI-Assisted Development

### The Pattern

1. **Describe** what you want to build
2. **Generate** code with AI
3. **Review** the output (especially auth and DB queries)
4. **Test** the functionality
5. **Iterate** with follow-up prompts

### Good Prompts

```
❌ Bad: "Build me a login page"

✅ Good: "Build a login page with:
- Email and password fields
- Form validation (email format, password 8+ chars)
- Error messages that don't reveal if email exists
- Loading state on submit
- Redirect to /dashboard on success
- Use Supabase Auth"
```

### What to Review Manually

Always review these yourself:

- [ ] Authentication logic
- [ ] Database queries (SQL injection risk)
- [ ] API permissions and scopes
- [ ] Error messages (don't leak info)
- [ ] Environment variable usage

---

## Project Ideas

| Project | Time | Stack |
|---------|------|-------|
| Dashboard with charts | 2 hrs | Next.js + Supabase + Recharts |
| Chrome extension | 2 hrs | Vanilla JS or React |
| API with auth | 3 hrs | Next.js API routes + Supabase |
| Blog with CMS | 3 hrs | Next.js + MDX or Sanity |

---

## Security Checklist

Before deploying:

- [ ] Secrets in `.env`, not in code
- [ ] `.env` in `.gitignore`
- [ ] Auth code reviewed manually
- [ ] Database queries use parameterized inputs
- [ ] Error messages don't expose internals
- [ ] API routes have proper auth checks
- [ ] Rate limiting on public endpoints

→ [Full Security Checklist](../security/checklist.md)

---

## Keyboard Shortcuts (Cursor)

| Action | Mac | Windows |
|--------|-----|---------|
| AI Chat | Cmd+L | Ctrl+L |
| Inline Edit | Cmd+K | Ctrl+K |
| Accept Suggestion | Tab | Tab |
| Reject Suggestion | Esc | Esc |
| Generate in Terminal | Cmd+K | Ctrl+K |

→ [Full Cheatsheet](../../cheatsheets/cursor-shortcuts.md)

---

## Next Steps

Once you're comfortable:

1. **Try agentic tools** - Claude Code, Kiro
2. **Learn MCP** - Connect AI to external tools
3. **Explore spec-driven development** - More structure, better results

→ [Advanced Guide](../advanced/README.md)

---

*You code. AI accelerates. That's the intermediate flow.*
