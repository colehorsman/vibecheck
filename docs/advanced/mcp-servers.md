# MCP Servers

Connect AI to the real world.

## TL;DR

- **MCP** = Model Context Protocol (open standard from Anthropic)
- **Purpose** = Let AI tools connect to external systems
- **Examples** = Databases, APIs, file systems, browsers
- **Supported by** = Claude Code, Kiro, Cline, Cursor

---

## What is MCP?

Model Context Protocol is an open standard that lets AI assistants connect to external tools and data sources.

Without MCP: AI can only see what you paste into the chat.

With MCP: AI can query databases, call APIs, read files, control browsers.

---

## How It Works

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   AI Tool   │ ←→  │ MCP Server  │ ←→  │  External   │
│ (Claude,    │     │ (adapter)   │     │  System     │
│  Kiro, etc) │     │             │     │ (DB, API)   │
└─────────────┘     └─────────────┘     └─────────────┘
```

The MCP server acts as a bridge between the AI and external systems.

---

## Configuration

### Claude Code

```json
// ~/.claude/mcp.json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["@supabase/mcp-server"],
      "env": {
        "SUPABASE_URL": "your-project-url",
        "SUPABASE_KEY": "your-anon-key"
      }
    }
  }
}
```

### Kiro

```json
// .kiro/settings/mcp.json
{
  "mcpServers": {
    "aws-docs": {
      "command": "uvx",
      "args": ["awslabs.aws-documentation-mcp-server@latest"],
      "disabled": false
    }
  }
}
```

### Cursor

```json
// .cursor/mcp.json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-filesystem", "/path/to/allowed"]
    }
  }
}
```

---

## Popular MCP Servers

### Official (Anthropic)

| Server | Purpose | Install |
|--------|---------|---------|
| **filesystem** | Read/write files | `@modelcontextprotocol/server-filesystem` |
| **github** | GitHub API access | `@modelcontextprotocol/server-github` |
| **postgres** | PostgreSQL queries | `@modelcontextprotocol/server-postgres` |
| **sqlite** | SQLite database | `@modelcontextprotocol/server-sqlite` |
| **puppeteer** | Browser automation | `@modelcontextprotocol/server-puppeteer` |

### AWS Labs

| Server | Purpose | Install |
|--------|---------|---------|
| **aws-docs** | AWS documentation | `awslabs.aws-documentation-mcp-server` |
| **bedrock** | Bedrock models | `awslabs.bedrock-mcp-server` |
| **cdk** | CDK operations | `awslabs.cdk-mcp-server` |

### Community

| Server | Purpose | Source |
|--------|---------|--------|
| **supabase** | Supabase operations | `@supabase/mcp-server` |
| **notion** | Notion API | Community |
| **slack** | Slack messaging | Community |
| **linear** | Linear issues | Community |

---

## Example: Supabase MCP

### Setup

```json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["@supabase/mcp-server"],
      "env": {
        "SUPABASE_URL": "https://xxx.supabase.co",
        "SUPABASE_KEY": "your-anon-key"
      }
    }
  }
}
```

### What AI Can Do

```
You: "Show me all users who signed up this week"

AI: [Queries Supabase via MCP]
    SELECT * FROM users 
    WHERE created_at > now() - interval '7 days'
    
    Found 23 users...
```

```
You: "Create a new table for blog posts"

AI: [Executes via MCP]
    CREATE TABLE posts (
      id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
      title text NOT NULL,
      content text,
      author_id uuid REFERENCES users(id),
      created_at timestamptz DEFAULT now()
    );
    
    Table created successfully.
```

---

## Example: GitHub MCP

### Setup

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_xxx"
      }
    }
  }
}
```

### What AI Can Do

```
You: "Create a PR for my current changes"

AI: [Via GitHub MCP]
    Created PR #42: "Add user authentication"
    https://github.com/user/repo/pull/42
```

```
You: "What issues are assigned to me?"

AI: [Queries GitHub API]
    Found 3 open issues:
    - #15: Fix login bug (high priority)
    - #18: Add dark mode
    - #21: Update documentation
```

---

## Example: Browser MCP (Puppeteer)

### Setup

```json
{
  "mcpServers": {
    "puppeteer": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-puppeteer"]
    }
  }
}
```

### What AI Can Do

```
You: "Take a screenshot of our landing page"

AI: [Controls browser via MCP]
    Navigating to https://example.com...
    Screenshot saved to ./screenshot.png
```

```
You: "Fill out the contact form with test data"

AI: [Automates browser]
    Filled name: "Test User"
    Filled email: "test@example.com"
    Clicked submit
    Form submitted successfully
```

---

## Security Considerations

### 1. Scope Permissions

Only enable servers you need:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "./src",  // Only allow src directory
        "./tests" // And tests directory
      ]
    }
  }
}
```

### 2. Use Read-Only When Possible

```json
{
  "mcpServers": {
    "postgres": {
      "env": {
        "DATABASE_URL": "postgres://readonly_user:xxx@host/db"
      }
    }
  }
}
```

### 3. Environment Variables for Secrets

Never hardcode credentials:

```json
{
  "mcpServers": {
    "supabase": {
      "env": {
        "SUPABASE_KEY": "${SUPABASE_KEY}"  // From environment
      }
    }
  }
}
```

### 4. Audit Logging

Enable logging to track what AI does:

```json
{
  "mcpServers": {
    "supabase": {
      "env": {
        "LOG_LEVEL": "debug"
      }
    }
  }
}
```

---

## Building Custom MCP Servers

### Basic Structure (TypeScript)

```typescript
import { Server } from "@modelcontextprotocol/sdk/server";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio";

const server = new Server({
  name: "my-custom-server",
  version: "1.0.0"
});

// Define a tool
server.setRequestHandler("tools/list", async () => ({
  tools: [{
    name: "my_tool",
    description: "Does something useful",
    inputSchema: {
      type: "object",
      properties: {
        input: { type: "string" }
      }
    }
  }]
}));

// Handle tool calls
server.setRequestHandler("tools/call", async (request) => {
  if (request.params.name === "my_tool") {
    const result = await doSomething(request.params.arguments.input);
    return { content: [{ type: "text", text: result }] };
  }
});

// Start server
const transport = new StdioServerTransport();
await server.connect(transport);
```

### Python Version

```python
from mcp.server import Server
from mcp.server.stdio import stdio_server

server = Server("my-custom-server")

@server.tool()
async def my_tool(input: str) -> str:
    """Does something useful"""
    result = await do_something(input)
    return result

async def main():
    async with stdio_server() as (read, write):
        await server.run(read, write)

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

---

## Troubleshooting

### Server Not Connecting

```bash
# Test server manually
npx @modelcontextprotocol/server-filesystem /tmp

# Check logs
tail -f ~/.claude/logs/mcp.log
```

### Permission Denied

```bash
# Ensure command is executable
which npx  # Should return path
which uvx  # For Python servers
```

### Environment Variables Not Loading

```bash
# Verify env vars are set
echo $SUPABASE_KEY

# Or use dotenv
source .env && claude
```

---

## Resources

- [MCP Specification](https://modelcontextprotocol.io)
- [Official Servers](https://github.com/modelcontextprotocol/servers)
- [AWS Labs MCP Servers](https://github.com/awslabs/mcp)
- [Community Servers](https://github.com/punkpeye/awesome-mcp-servers)

---

*Connect AI to your tools. Safely.*
