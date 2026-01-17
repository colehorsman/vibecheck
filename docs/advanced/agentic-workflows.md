# Agentic Workflows

Let AI drive. You supervise.

## TL;DR

- **Agentic** = AI takes actions autonomously
- **Multi-agent** = specialized agents working together
- **Human-in-the-loop** = you approve critical actions
- **Tools:** Claude Code, Kiro, Cline, Devin

---

## What is Agentic Coding?

Traditional AI coding: You prompt → AI suggests → You accept/reject

Agentic coding: You describe goal → AI plans → AI executes → You review

The AI doesn't just suggest code. It:
- Reads your codebase
- Plans the implementation
- Writes files
- Runs tests
- Fixes errors
- Commits changes

You supervise. AI drives.

---

## Agentic Tools Comparison

| Tool | Autonomy Level | Best For |
|------|----------------|----------|
| **Claude Code** | High | Full-stack development, complex tasks |
| **Kiro** | Medium-High | Spec-driven, enterprise workflows |
| **Cline** | High | Open-source, customizable |
| **Cursor Composer** | Medium | Multi-file edits |
| **Devin** | Very High | Fully autonomous (expensive) |

---

## Claude Code Agentic Features

### Autonomous Mode

```bash
# Let Claude Code work autonomously
claude --dangerously-skip-permissions

# Or configure in settings
claude config set autoApprove "bash(npm test),bash(npm run lint)"
```

### What It Can Do Autonomously

- Read/write files
- Run terminal commands
- Search codebase
- Install packages
- Run tests
- Fix failing tests

### What Requires Approval (by default)

- Destructive commands (rm, git push)
- Network requests
- Sensitive file access
- Production deployments

---

## Kiro Agentic Features

### Autopilot Mode

Kiro has two modes:
- **Supervised:** Review each change before applying
- **Autopilot:** AI applies changes automatically

### Hooks System

Automate agent actions based on events:

```json
{
  "name": "Lint on Save",
  "when": {
    "type": "fileEdited",
    "patterns": ["*.ts", "*.tsx"]
  },
  "then": {
    "type": "askAgent",
    "prompt": "Run npm run lint and fix any errors"
  }
}
```

### Multi-Agent Workflows

Kiro supports specialized sub-agents:
- **Context Gatherer:** Analyzes codebase
- **Spec Executor:** Implements from specs
- **Task Runner:** Executes specific tasks

---

## Multi-Agent Patterns

### Pattern 1: Planner + Executor

```
User Request
    ↓
Planner Agent (breaks into tasks)
    ↓
Executor Agent (implements each task)
    ↓
Reviewer Agent (validates output)
```

### Pattern 2: Specialist Agents

```
User Request
    ↓
Router Agent (determines specialist)
    ↓
┌─────────────────────────────────┐
│ Frontend Agent │ Backend Agent │
│ Database Agent │ Test Agent    │
└─────────────────────────────────┘
    ↓
Integrator Agent (combines work)
```

### Pattern 3: Iterative Refinement

```
User Request
    ↓
Draft Agent (initial implementation)
    ↓
Critic Agent (identifies issues)
    ↓
Refine Agent (fixes issues)
    ↓
[Loop until quality threshold met]
```

---

## Human-in-the-Loop Patterns

### Approval Gates

Critical actions require human approval:

```
AI: "I need to delete the users table and recreate it. Approve? [y/n]"
Human: Reviews, approves or rejects
```

### Checkpoint Reviews

Pause at milestones for review:

```
1. Requirements → [Human Review] ✓
2. Design → [Human Review] ✓
3. Implementation → [Human Review] ✓
4. Tests → [Human Review] ✓
5. Deploy → [Human Review] ✓
```

### Confidence Thresholds

AI proceeds autonomously when confident, asks when uncertain:

```
High confidence (>90%): Auto-proceed
Medium confidence (70-90%): Proceed with notification
Low confidence (<70%): Ask for guidance
```

---

## MCP Integration

Model Context Protocol enables agents to:
- Connect to external tools
- Access databases
- Call APIs
- Control browsers
- Manage files

```json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["@supabase/mcp-server"]
    },
    "github": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-github"]
    }
  }
}
```

→ [MCP Servers Guide](mcp-servers.md)

---

## Safety Guardrails

### 1. Scope Permissions

Only grant access to what's needed:

```json
{
  "permissions": {
    "fileSystem": ["src/**", "tests/**"],
    "commands": ["npm test", "npm run lint"],
    "network": false
  }
}
```

### 2. Audit Everything

Log all agent actions:

```
[2026-01-17 10:23:45] Agent: Read file src/auth/login.ts
[2026-01-17 10:23:47] Agent: Modified src/auth/login.ts (lines 45-67)
[2026-01-17 10:23:50] Agent: Ran command: npm test
```

### 3. Sandbox Environments

Test in isolation before production:

```bash
# Create isolated environment
docker run -it --rm -v $(pwd):/app node:20

# Agent works in sandbox
# Human reviews before merging
```

### 4. Rollback Capability

Always be able to undo:

```bash
# Git provides natural rollback
git diff HEAD~1  # Review changes
git revert HEAD  # Undo if needed
```

---

## When to Use Agentic

### Good Use Cases

- ✅ Boilerplate generation
- ✅ Test writing
- ✅ Refactoring
- ✅ Documentation
- ✅ Bug fixes with clear reproduction
- ✅ Feature implementation from specs

### Use with Caution

- ⚠️ Security-critical code
- ⚠️ Database migrations
- ⚠️ Production deployments
- ⚠️ Financial calculations
- ⚠️ Authentication/authorization

### Avoid

- ❌ Unsupervised production access
- ❌ Handling secrets directly
- ❌ Critical infrastructure changes
- ❌ Compliance-sensitive operations

---

## Getting Started

### 1. Start Supervised

Begin with full human review:

```bash
# Claude Code with approval required
claude "Implement user authentication"
# Review each file change before accepting
```

### 2. Gradually Increase Autonomy

As you build trust:

```bash
# Auto-approve safe commands
claude config set autoApprove "bash(npm test)"
```

### 3. Define Clear Boundaries

Document what AI can/cannot do:

```markdown
## AI Permissions

### Allowed
- Read/write src/** and tests/**
- Run npm test, npm run lint
- Create new files in allowed directories

### Requires Approval
- Modify package.json
- Run npm install
- Access .env files

### Forbidden
- Production deployments
- Database migrations
- Secret management
```

---

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Kiro Hooks Guide](https://kiro.dev/docs/hooks)
- [MCP Specification](https://modelcontextprotocol.io)
- [Cline GitHub](https://github.com/cline/cline)

---

*Trust but verify. Automate but supervise.*
