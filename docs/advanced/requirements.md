# Advanced Requirements

What you need for agentic AI development.

## Essential (Required)

- [ ] **Full-stack development experience** - Frontend + backend
- [ ] **API integration experience** - REST, GraphQL, or similar
- [ ] **Git proficiency** - Branching, merging, PRs
- [ ] **Terminal comfort** - Command line is your friend
- [ ] **Previous AI tool experience** - Cursor, Copilot, or similar

## Recommended

- [ ] **Claude Code CLI** - `npm install -g @anthropic-ai/claude-code`
- [ ] **Kiro** - Download from [kiro.dev](https://kiro.dev)
- [ ] **MCP understanding** - [modelcontextprotocol.io](https://modelcontextprotocol.io)
- [ ] **2-4 hours** - For setup and first agentic project

## Nice to Have

- [ ] AWS account (for MCP servers)
- [ ] Docker experience
- [ ] CI/CD pipeline experience
- [ ] Security scanning tools

---

## Setup Checklist

### 1. Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
claude-code auth
```

### 2. Install Kiro

Download from [kiro.dev](https://kiro.dev). Sign in with:
- AWS account
- GitHub account
- Google account

### 3. Set Up MCP (Optional)

```bash
# Install UV for Python MCP servers
curl -LsSf https://astral.sh/uv/install.sh | sh

# Test with AWS docs server
uvx awslabs.aws-documentation-mcp-server@latest
```

### 4. Configure Environment

```bash
# Create project structure
mkdir my-agentic-project
cd my-agentic-project

# Initialize
git init
npm init -y

# Create CLAUDE.md
touch CLAUDE.md

# Create Kiro steering
mkdir -p .kiro/steering
touch .kiro/steering/project-context.md
```

---

## Knowledge Prerequisites

### Must Know
- TypeScript/JavaScript
- React or similar framework
- Database concepts (SQL, NoSQL)
- API design principles
- Git workflows

### Should Know
- Docker basics
- CI/CD concepts
- Security fundamentals
- Cloud services (AWS, Vercel, etc.)

### Nice to Know
- Terraform/IaC
- Kubernetes basics
- Advanced security (OWASP, etc.)
- Performance optimization

---

## Project Ideas by Complexity

### Level 1: Agentic Basics (2-4 hours)
- Autonomous code refactoring
- Multi-file feature implementation
- Automated test generation

### Level 2: MCP Integration (4-8 hours)
- AI connected to AWS services
- Database-aware code generation
- Browser automation tasks

### Level 3: Production Systems (8+ hours)
- Full spec-driven application
- Multi-agent orchestration
- CI/CD with AI code review

---

## Pre-Session Checklist

Before an advanced Vibeations session:

- [ ] Claude Code CLI installed and authenticated
- [ ] Kiro installed and signed in
- [ ] MCP basics understood
- [ ] Project idea with clear scope
- [ ] 3+ hours of uninterrupted time

**Ready?** → [Start Building](README.md)
