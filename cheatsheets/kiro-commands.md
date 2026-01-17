# Kiro Commands Cheatsheet

Print this. Keep it handy.

## Keyboard Shortcuts

| Action | Mac | Windows |
|--------|-----|---------|
| **Command Palette** | `Cmd+Shift+P` | `Ctrl+Shift+P` |
| **New Spec** | `Cmd+Shift+N` | `Ctrl+Shift+N` |
| **Chat with Kiro** | `Cmd+L` | `Ctrl+L` |
| **Accept Suggestion** | `Tab` | `Tab` |
| **Reject Suggestion** | `Esc` | `Esc` |

## Command Palette Commands

| Command | What It Does |
|---------|--------------|
| `Kiro: New Spec` | Create new feature spec |
| `Kiro: Open Spec` | Open existing spec |
| `Kiro: Run Tasks` | Execute spec tasks |
| `Kiro: Create Steering` | Create steering file |

## Spec Structure

```markdown
# Feature: [Name]

## Requirements
- [EARS format requirements]

## Design
### Components
- [Component list]

### Data Flow
1. [Step 1]
2. [Step 2]

## Tasks
- [ ] Task 1
- [ ] Task 2
```

## EARS Format

| Pattern | Template |
|---------|----------|
| **Ubiquitous** | The system shall [action] |
| **Event-driven** | When [trigger], the system shall [action] |
| **State-driven** | While [state], the system shall [action] |
| **Optional** | Where [condition], the system shall [action] |
| **Unwanted** | If [condition], the system shall [action] |

**Example:**
```markdown
**Event-driven:** When user clicks login, the system shall validate credentials.
**Unwanted:** If credentials are invalid, the system shall display error.
```

## Steering Files

Create in `.kiro/steering/`:

```markdown
# .kiro/steering/project-context.md
---
inclusion: always
---

## Tech Stack
- Next.js 14
- Supabase
- TypeScript
```

### Inclusion Modes

| Mode | When Included |
|------|---------------|
| `always` | Every interaction |
| `fileMatch` | When matching files in context |
| `manual` | Only when referenced with # |

## Hooks

Create in `.kiro/hooks/`:

```json
{
  "name": "Lint on Save",
  "version": "1.0.0",
  "when": {
    "type": "fileEdited",
    "patterns": ["*.ts", "*.tsx"]
  },
  "then": {
    "type": "askAgent",
    "prompt": "Run npm run lint and fix errors"
  }
}
```

### Hook Events

| Event | Trigger |
|-------|---------|
| `fileEdited` | File saved |
| `fileCreated` | New file created |
| `fileDeleted` | File deleted |
| `promptSubmit` | Message sent |
| `agentStop` | Agent completes |
| `userTriggered` | Manual trigger |

## Pro Tips

1. **Start with requirements** - Good specs = good code
2. **Use steering files** - Persistent context saves tokens
3. **Review before approve** - Check each spec section
4. **Small tasks** - Break into <1 hour chunks

---

*Cmd+Shift+N for new spec. Cmd+L to chat.*
