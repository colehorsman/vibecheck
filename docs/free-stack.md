# The $0 Vibe Coding Stack

Build production apps without spending a dime.

## TL;DR

| Need | Use This | Cost |
|------|----------|------|
| IDE | Google AntiGravity | $0 |
| Database | Supabase | $0 |
| Auth | Stack Auth | $0 |
| LLM | Gemini AI Studio | $0 |
| Deploy | Vercel | $0 |
| Analytics | PostHog + Clarity | $0 |
| **Total** | | **$0** |

Build first. Pay later (when you have revenue).

---

## Why This Matters

Typical vibe coding costs:
- Cursor/Lovable: $20-50/mo
- API costs: $50-200/mo
- Hosting: $20-50/mo
- **Total: $100-300/mo**

This stack: **$0/mo** (with generous free tiers)

---

## The Complete Stack

### Layer 1: IDE

**Option A: Google AntiGravity (Recommended)**
- Cost: Free during public preview
- Features: Multi-agent, Gemini 3 Pro, Claude Sonnet 4.5
- Best for: Agent-first development

**Option B: VS Code + Free Extensions**
- Kilo Code (Roo + Cline combined)
- Gemini CLI (free terminal access)
- Continue (open source Copilot)

**Option C: Emergent**
- Cursor-like experience, free tier

### Layer 2: Database

**Supabase (Recommended)**
- Free: 500MB storage, 2 projects, 50K MAU
- Includes: Postgres, realtime, Row Level Security, auto APIs

**Alternatives:**
| Tool | Free Tier | Best For |
|------|-----------|----------|
| Neon | 512MB, 3 projects | Serverless Postgres |
| Turso | 9GB, 500 DBs | Edge SQLite |
| PlanetScale | 5GB, 1B reads/mo | MySQL |
| Firebase | Spark plan | Realtime, mobile |

### Layer 3: Authentication

**Stack Auth (Recommended)**
- Free: 10K users
- Features: OAuth, magic links, organizations, self-hostable
- Open source (MIT/AGPL)

**Alternatives:**
| Tool | Free Tier | Notes |
|------|-----------|-------|
| Supabase Auth | 50K MAU | Bundled with DB |
| WorkOS AuthKit | 1M users | Enterprise features |
| Lucia | Unlimited | Self-hosted |
| Auth.js | Unlimited | DIY |

### Layer 4: LLM / AI Models

**For Testing: Gemini AI Studio**
- Free tier with generous limits
- Great for prototyping

**For Production: OpenRouter**
- Pay-as-you-go (very cheap)
- Access to multiple models

**Free Options:**
| Provider | Free Tier |
|----------|-----------|
| Gemini | 60 req/min |
| Groq | 30 req/min |
| Ollama | Unlimited (local) |
| LM Studio | Unlimited (local) |

### Layer 5: Deployment

**Vercel (Recommended)**
- Free: 100GB bandwidth, 6K build minutes
- Perfect for Next.js

**Alternatives:**
| Platform | Free Tier |
|----------|-----------|
| Netlify | 100GB bandwidth |
| Cloudflare Pages | Unlimited |
| Railway | $5 credit/mo |
| Fly.io | 3 shared VMs |

### Layer 6: Analytics

Use all three (they're complementary):

- **PostHog** - Product analytics, feature flags (1M events/mo free)
- **Microsoft Clarity** - Session recordings, heatmaps (100% free)
- **Google Analytics 4** - Traffic, demographics (free)

---

## Quick Setup

```bash
# 1. Create project
mkdir my-app && cd my-app
npx create-next-app@latest . --typescript

# 2. Add Supabase
npm install @supabase/supabase-js

# 3. Add Stack Auth
npm install @stackframe/stack

# 4. Add analytics
npm install posthog-js

# 5. Deploy
vercel

# Total cost: $0
```

---

## When to Upgrade

Stay free until you hit these limits:

| Trigger | Action | Cost |
|---------|--------|------|
| 500+ MB database | Upgrade Supabase | $25/mo |
| 10K+ users | Upgrade Stack Auth | Varies |
| 100GB+ bandwidth | Upgrade Vercel | $20/mo |
| Production LLM | Budget for OpenRouter | $50-100/mo |

**Rule of thumb:** Stay free until you have paying customers.

---

## Security Checklist (Free Tier)

Even on free tiers, follow security basics:

- [ ] Environment variables for all secrets
- [ ] `.env` in `.gitignore`
- [ ] Row Level Security enabled (Supabase)
- [ ] HTTPS everywhere (automatic on Vercel)
- [ ] Rate limiting on APIs
- [ ] Input validation
- [ ] No secrets in client-side code

---

## Token Optimization

Even with free tiers, optimize your AI usage:

**The 10-15% Rule:** Use only 10-15% of context per request.

| Technique | Savings |
|-----------|---------|
| TOON format for arrays | 30-60% |
| Specific file references | 40-80% |
| Steering files (Kiro) | Avoids repetition |
| Focused prompts | Better accuracy |

→ [Token Optimization Guide](advanced/token-optimization.md)

---

*Build first. Pay later.*
