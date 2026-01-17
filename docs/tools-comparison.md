# AI Coding Tools Comparison

Find the right tool for your level and use case.

## Quick Reference

| Tool | Level | Cost | Best For |
|------|-------|------|----------|
| [Lovable](https://lovable.dev) | Beginner | Free tier | Describe → Build |
| [v0](https://v0.dev) | Beginner | Free tier | UI components |
| [Bolt.new](https://bolt.new) | Beginner | Free tier | Quick prototypes |
| [Replit](https://replit.com) | Beginner | Free tier | Browser IDE |
| [Cursor](https://cursor.com) | Intermediate | $20/mo | Best overall |
| [Windsurf](https://codeium.com/windsurf) | Intermediate | Free | Cursor alternative |
| [GitHub Copilot](https://github.com/features/copilot) | Intermediate | $10/mo | Best value |
| [Claude Code](https://claude.ai/code) | Advanced | Usage-based | Agentic coding |
| [Kiro](https://kiro.dev) | Advanced | Free preview | Spec-driven |
| [Cline](https://github.com/cline/cline) | Advanced | Free | Open-source agent |

---

## Beginner Tools

### Lovable
- **Website:** [lovable.dev](https://lovable.dev)
- **Cost:** Free tier available
- **Best for:** Full apps from natural language
- **How it works:** Describe your app, watch it build
- **Limitations:** Less control over code structure

### v0 (Vercel)
- **Website:** [v0.dev](https://v0.dev)
- **Cost:** Free tier available
- **Best for:** UI components and dashboards
- **How it works:** Describe UI, get React/Tailwind code
- **Limitations:** UI-focused, not full apps

### Bolt.new
- **Website:** [bolt.new](https://bolt.new)
- **Cost:** Free tier available
- **Best for:** Quick web app prototypes
- **How it works:** Browser-based, instant preview
- **Limitations:** Simpler projects only

### Replit
- **Website:** [replit.com](https://replit.com)
- **Cost:** Free tier available
- **Best for:** Learning with AI assistance
- **How it works:** Browser IDE with Ghostwriter AI
- **Limitations:** AI features limited on free tier

---

## Intermediate Tools

### Cursor
- **Website:** [cursor.com](https://cursor.com)
- **Cost:** $20/month (free trial)
- **Best for:** Daily development with AI
- **How it works:** VS Code fork with native AI
- **Key features:**
  - Cmd+K for inline edits
  - Cmd+L for chat
  - Codebase-aware suggestions
  - .cursorrules for project context
- **Why it's popular:** Best balance of control and AI power

### Windsurf (Codeium)
- **Website:** [codeium.com/windsurf](https://codeium.com/windsurf)
- **Cost:** Free
- **Best for:** Cursor alternative without cost
- **How it works:** Similar to Cursor, different AI backend
- **Limitations:** Newer, less mature

### GitHub Copilot
- **Website:** [github.com/features/copilot](https://github.com/features/copilot)
- **Cost:** $10/month (free for students)
- **Best for:** Inline suggestions while coding
- **How it works:** Tab to accept suggestions
- **Key features:**
  - Works in any IDE
  - Copilot Chat for questions
  - PR summaries
- **Limitations:** Less autonomous than Cursor

---

## Advanced Tools

### Claude Code
- **Website:** [claude.ai/code](https://claude.ai/code)
- **Cost:** Usage-based (Anthropic API)
- **Best for:** Autonomous coding tasks
- **How it works:** Agentic AI that executes tasks
- **Key features:**
  - Multi-file changes
  - Terminal access
  - MCP integration
  - CLAUDE.md for project context
- **When to use:** Complex refactoring, multi-step tasks

### Kiro (AWS)
- **Website:** [kiro.dev](https://kiro.dev)
- **Cost:** Free during preview
- **Best for:** Spec-driven development
- **How it works:** Requirements → Design → Tasks → Code
- **Key features:**
  - EARS format for requirements
  - Steering files for context
  - Hooks for automation
  - Built-in documentation
- **When to use:** Production systems, team projects

### Cline
- **Website:** [github.com/cline/cline](https://github.com/cline/cline)
- **Cost:** Free (bring your own API key)
- **Best for:** Open-source agentic coding
- **How it works:** VS Code extension with agent capabilities
- **Limitations:** Requires API key setup

---

## Comparison Matrix

| Feature | Lovable | Cursor | Claude Code | Kiro |
|---------|---------|--------|-------------|------|
| No-code friendly | ✅ | ❌ | ❌ | ❌ |
| Inline suggestions | ❌ | ✅ | ❌ | ✅ |
| Autonomous tasks | ❌ | Partial | ✅ | ✅ |
| Spec-driven | ❌ | ❌ | ❌ | ✅ |
| MCP support | ❌ | ❌ | ✅ | ✅ |
| Free tier | ✅ | Trial | ❌ | ✅ |
| Best for | Beginners | Daily dev | Complex tasks | Production |

---

## Decision Tree

```
Are you new to coding?
├── Yes → Start with Lovable or v0
└── No
    ├── Do you want AI suggestions while you code?
    │   ├── Yes → Cursor or GitHub Copilot
    │   └── No, I want AI to do more
    │       ├── Do you need documentation/specs?
    │       │   ├── Yes → Kiro
    │       │   └── No → Claude Code
    │       └── Do you want free/open-source?
    │           └── Yes → Cline
```

---

## Resources

- [awesome-vibe-coding](https://github.com/filipecalegario/awesome-vibe-coding) - Comprehensive list
- [awesome-cursorrules](https://github.com/PatrickJS/awesome-cursorrules) - Cursor configs
- [awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) - MCP servers

---

*Pick one. Start building. Upgrade when you need to.*
