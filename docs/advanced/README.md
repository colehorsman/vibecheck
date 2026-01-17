# Advanced Guide

Ready for agentic AI. Let it drive.

## TL;DR

1. Use **Claude Code** or **Kiro** for autonomous coding
2. Apply the **10-15% context rule** for better results
3. Use **spec-driven development** for production systems
4. Connect to external tools via **MCP**

---

## Requirements

Before you start:

- [ ] Comfortable with full-stack development
- [ ] Understanding of APIs and integrations
- [ ] Experience with at least one AI coding tool
- [ ] Ready to let AI make decisions

→ [Full Requirements](requirements.md)

---

## Recommended Tools

| Tool | Cost | Best For |
|------|------|----------|
| **Claude Code** | Usage-based | Agentic coding, autonomous tasks |
| **Kiro** | Free preview | Spec-driven development |
| **Cline** | Free | Open-source agent |

---

## Key Concepts

### 1. Token Optimization

**The 10-15% Rule:** Use only 10-15% of the model's context window per request.

**Why it matters:**
- Accuracy drops from 75% → 55% when info is buried in 4K+ tokens
- Smaller, focused context = better results
- Saves money on API costs

**Techniques:**
| Technique | Savings |
|-----------|---------|
| TOON format for arrays | 30-60% |
| Specific file references | 40-80% |
| Steering files (Kiro) | Avoids repetition |
| Focused prompts | Better accuracy |

→ [Token Optimization Guide](token-optimization.md)

### 2. Spec-Driven Development

Structure your intent before AI writes code.

```
Idea → Requirements → Design → Tasks → Code → Tests
```

**EARS Format for Requirements:**

| Pattern | Template |
|---------|----------|
| Ubiquitous | The system shall [action] |
| Event-driven | When [trigger], the system shall [action] |
| State-driven | While [state], the system shall [action] |
| Optional | Where [condition], the system shall [action] |
| Unwanted | If [condition], the system shall [action] |

→ [Spec-Driven Development Guide](spec-driven.md)

### 3. MCP Integration

Model Context Protocol connects AI to external tools.

**Available MCP Servers:**
- AWS services (S3, DynamoDB, etc.)
- Supabase
- GitHub
- Filesystem
- Browser automation
- Custom APIs

→ [MCP Servers Guide](mcp-servers.md)

### 4. Agentic Workflows

Let AI orchestrate multiple tasks.

**Patterns:**
- **Single agent:** One AI handles everything
- **Multi-agent:** Specialized agents for different tasks
- **Human-in-the-loop:** AI proposes, human approves

→ [Agentic Workflows Guide](agentic-workflows.md)

---

## Claude Code Setup

### Installation

```bash
# Install Claude Code CLI
npm install -g @anthropic-ai/claude-code

# Authenticate
claude-code auth
```

### CLAUDE.md Configuration

Create `CLAUDE.md` in your project root:

```markdown
# Project: [Name]

## Tech Stack
- Framework: Next.js 14
- Database: Supabase
- Language: TypeScript

## Commands
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run test` - Run tests

## Architecture
- `/app` - Next.js app router pages
- `/components` - React components
- `/lib` - Utility functions
- `/supabase` - Database types and client

## Security Rules
- Never hardcode secrets
- Use environment variables
- Validate all inputs
- Use parameterized queries
```

### Usage

```bash
# Start a session
claude-code

# Or run a specific task
claude-code "Add user authentication with Supabase"
```

---

## Kiro Setup

### Installation

Download from [kiro.dev](https://kiro.dev). Sign in with AWS, GitHub, or Google.

### Creating a Spec

1. Open Command Palette (Cmd+Shift+P)
2. Select "Kiro: New Spec"
3. Describe your feature
4. Review generated requirements
5. Approve and let Kiro implement

### Steering Files

Create `.kiro/steering/` files for persistent context:

```markdown
# .kiro/steering/project-context.md
---
inclusion: always
---

## Tech Stack
- Next.js 14 with App Router
- Supabase for database and auth
- Tailwind CSS for styling
- TypeScript strict mode

## Patterns
- Server components by default
- Client components only when needed
- Zod for validation
```

---

## Project Ideas

| Project | Complexity | Tools |
|---------|------------|-------|
| Multi-agent research system | High | Claude Code + MCP |
| Full-stack app with specs | High | Kiro |
| API integration platform | Medium | Claude Code |
| Automated testing suite | Medium | Kiro + PBT |

---

## Security at Scale

For production systems:

- [ ] Scoped permissions for AI (read-only where possible)
- [ ] Audit trails for all AI actions
- [ ] Human review for security-critical code
- [ ] Time-limited access (JIT principles)
- [ ] Automated security scanning in CI/CD

→ [Deployment Security Stages](../security/deployment-stages.md)

---

## Next Steps

1. **Master token optimization** - Biggest ROI for advanced users
2. **Build with specs** - Better results, better documentation
3. **Explore MCP** - Connect AI to your entire stack
4. **Contribute** - Share what you learn

---

*You guide. AI executes. That's agentic coding.*
