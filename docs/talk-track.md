# Vibeations Talk Track

**Sip. Build. Secure.**

Duration: 90 minutes | Format: Learn + Build + Share

---

## Timing Summary

| Time | Section | Duration |
|------|---------|----------|
| 0:00 | **Sip** - Opening & Intros | 10 min |
| 0:10 | **Learn** - What is Vibe Coding? | 5 min |
| 0:15 | **Tools** - Find Your Starting Point | 10 min |
| 0:25 | **Secure** - Low-Hanging Fruit Security | 10 min |
| 0:35 | **Build** - Hands-On Build Time | 30 min |
| 1:05 | **Demo** - The Video Game | 10 min |
| 1:15 | **Share** - What Did You Build? | 10 min |
| 1:25 | **Wrap** - Resources & GitHub Repo | 5 min |

---

## Sip: Opening & Intros (10 min)

"Welcome to Vibeations. Sip. Build. Secure. Grab a drink if you haven't already."

"By the end of this session, you'll leave with:"
- Basic skills to vibe code a project
- A GitHub repo of helpful resources → **github.com/vibeations/vibeations**
- Working code (if you brought a project idea)
- The security checklist that prevents 80% of disasters

**Quick show of hands:**
- "Who has never written code?"
- "Who codes but hasn't used AI tools much?"
- "Who uses AI coding tools daily?"

---

## Learn: What is Vibe Coding? (5 min)

"February 2025. Andrej Karpathy tweets about 'vibe coding.' By December, Collins Dictionary names it Word of the Year."

**The idea:**
1. Describe what you want in plain English
2. AI generates the code
3. You test and iterate
4. You guide. AI types.

**The security reality:**
> "80% of AI-generated code contains vulnerabilities."

That's why we're covering security BEFORE you build.

---

## Tools: Find Your Starting Point (10 min)

| Your Level | Use This | Why |
|------------|----------|-----|
| Never coded | Lovable or v0 | Zero setup, describe and build |
| Some experience | Cursor | Best overall AI IDE |
| Already using AI | Claude Code or Kiro | Agentic, autonomous |

**$0 Stack Available:**
- IDE: Google AntiGravity (free preview)
- Database: Supabase (free tier)
- Auth: Stack Auth (10K users free)
- Deploy: Vercel (free tier)

→ Full guide: **github.com/vibeations/vibeations/docs/free-stack.md**

---

## Secure: Low-Hanging Fruit (10 min)

**The 7-point checklist that prevents 80% of disasters:**

1. **Never commit secrets.** Use `.env` files.
2. **Review auth code.** AI often skips it.
3. **Check .gitignore.** AI doesn't always know what to exclude.
4. **Scope API permissions.** Only what's needed.
5. **Use secrets scanner.** git-secrets, gitleaks.
6. **Review DB queries.** SQL injection is real.
7. **Test error handling.** Don't expose stack traces.

→ Printable checklist: **github.com/vibeations/vibeations/docs/security/checklist.md**

---

## Build: Hands-On Time (30 min)

**Rules:**
1. Ask for help. Mentors are circulating.
2. Start small. Get something working first.
3. Use the security checklist. Set up `.env` before adding API keys.
4. It's okay to follow along.

**Starter projects if you need one:**

| Project | Tool | Time |
|---------|------|------|
| Personal portfolio | Lovable | 20 min |
| Landing page | v0 | 15 min |
| Dashboard | Cursor + Supabase | 30 min |

---

## Demo: The Video Game (10 min)

"A few months ago, I built a video game. AI wrote 90% of the code."

**What made it work:**
- **Scoped permissions.** AI only accessed what it needed.
- **Audit trail.** Every API call logged.
- **Human review.** Integration points reviewed manually.
- **Time-limited access.** JIT principles applied to AI.

"This isn't a toy demo. It's a working application that proves governance is possible."

---

## Share: What Did You Build? (10 min)

Invite 3-5 people to share for 1-2 minutes each.

**Questions to ask:**
- "What were you trying to build?"
- "Which tool did you use?"
- "What surprised you?"

---

## Wrap: Resources & GitHub Repo (5 min)

**The GitHub Repo:**

```
github.com/vibeations/vibeations
├── docs/
│   ├── free-stack.md        # $0 setup guide
│   ├── beginner/            # Never coded before
│   ├── intermediate/        # Know some code
│   ├── advanced/            # Agentic AI
│   │   ├── token-optimization.md
│   │   ├── spec-driven.md
│   │   └── mcp-servers.md
│   └── security/
│       ├── checklist.md     # The 7-point checklist
│       └── deployment-stages.md
├── configs/                 # .cursorrules, CLAUDE.md templates
├── cheatsheets/             # Print these!
└── starters/                # Project templates
```

**What you leave with:**
- ✅ Basic skills to vibe code a project
- ✅ A GitHub repo of resources
- ✅ Your own project (keep building!)
- ✅ A security-first mindset

---

## Q&A Framework

**"Which tool should I start with?"**
→ The one you'll actually use. Lovable for beginners, Cursor for devs, Claude Code for autonomy.

**"Is this secure?"**
→ It can be. Security depends on governance: scoped permissions, audit trails, human review.

**"Should we ban AI coding tools?"**
→ You can try. Your developers will use them anyway. Better to govern than to ban.

**"What's the biggest mistake you see?"**
→ Trusting AI with secrets. Hardcoded credentials, API keys in code. Use the checklist.

---

## Key Moments

1. **The 80% stat** — Sets the security frame
2. **The tool spectrum** — Permission to start where you are
3. **The 7-point checklist** — Practical takeaway
4. **The video game demo** — Proof you practice what you preach
5. **The GitHub repo** — Resources to keep going

---

*Sip. Build. Secure.*

**Resources:**
- GitHub: github.com/vibeations/vibeations
- Kiro: kiro.dev
- Claude Code: claude.ai/code
- MCP: modelcontextprotocol.io
