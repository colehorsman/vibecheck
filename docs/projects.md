# 🎨 Example Projects

Real projects built with vibe coding and spec engineering. All use the $0 stack.

---

## 1. 💰 FinTracker — AI-Powered Financial Command Center

Personal finance dashboard that downloads transactions from financial institutions, uses AI to categorize spending, and provides intelligent insights. Replaces the need for TurboTax, RocketMoney, and manual spreadsheets.

**Stack:**
- React + TypeScript (Frontend)
- Supabase (Database & Auth)
- OpenAI API (AI categorization)
- MCP (Model Context Protocol)

**Features:**
- Automatic transaction download from banks
- AI-powered expense categorization
- Tax preparation assistance
- Budget tracking and insights
- Multi-account aggregation

**Status:** Active Development

---

## 2. 🎮 Zombie Blaster — Gamified Cloud Security Training

Interactive arcade-style game that teaches cloud security concepts by connecting to real Sonrai Security APIs. Players "zap zombies" which triggers actual IAM identity quarantine actions in AWS. Demoed at AWS re:Invent where Jeff Barr stopped by!

**Stack:**
- Python
- Pygame (Game engine)
- Sonrai Security API

**Features:**
- Real-time integration with Sonrai Security platform
- Gamified learning for cloud security concepts
- Actual IAM identity quarantine on "kills"
- Leaderboard and scoring system
- Conference demo-ready

**Status:** Complete (Demo)

---

## 3. 🍽️ FeastIQ — AI-Native Smart Nutrition

Mobile app that finally answers "what's for dinner?" using advanced RAG (Retrieval Augmented Generation) to suggest meals based on dietary preferences, available ingredients, and nutritional goals. Features AI-generated food photography using Nova Canvas.

**Stack:**
- React Native (Mobile)
- AWS Bedrock (AI/ML)
- Terraform (Infrastructure)
- Nova Canvas (AI image generation)

**Features:**
- Personalized meal recommendations
- Ingredient-based recipe suggestions
- Nutritional tracking and goals
- AI-generated food photography
- Advanced RAG for context-aware suggestions

**Status:** Active Development

---

## 4. 🛡️ Security Agent — AI-Powered AWS Remediation

Autonomous AI agent that detects and auto-fixes AWS security misconfigurations. Maps findings to OWASP Top 10 and MITRE ATT&CK frameworks for comprehensive security coverage.

**Stack:**
- Python
- Strands Agent SDK
- Terraform
- AWS APIs

**Features:**
- Automated security misconfiguration detection
- One-click remediation actions
- OWASP Top 10 mapping
- MITRE ATT&CK framework integration
- Audit trail and compliance reporting

**GitHub:** [github.com/colehorsman/security-agent](https://github.com/colehorsman/security-agent)

**Status:** Active Development

---

## 5. 📊 re:Inforce Dashboard — AI Conference Summarizer

Dashboard that summarizes all 163 AWS re:Inforce conference talks using AI. Provides searchable summaries, key takeaways, and topic clustering for security professionals who couldn't attend every session.

**Stack:**
- PostgreSQL (Database)
- AI/ML (Summarization)

**Features:**
- 163 conference talks summarized
- Searchable talk database
- Key takeaways extraction
- Topic clustering and categorization
- Speaker and session metadata

**GitHub:** [github.com/colehorsman/aws-reinforce-dashboard](https://github.com/colehorsman/aws-reinforce-dashboard)

**Status:** Complete

---

## 6. 🤖 ATLAS — Autonomous Sales Intelligence

AI-powered sales intelligence platform that visualizes LinkedIn connections, syncs with Salesforce, and provides MEDDIC scoring for deals. Features autonomous AI agents for meeting preparation and deal risk alerts.

**Stack:**
- TypeScript + React (Frontend)
- Supabase (Database & Auth)
- MCP (Model Context Protocol)

**Features:**
- LinkedIn network visualization
- Salesforce CRM sync
- MEDDIC deal scoring
- AI meeting prep agents
- Deal risk alerts and notifications
- Relationship mapping

**Status:** Active Development

---

## 7. 📄 Modern CV — AI Career Showcase Platform

TypeScript platform that generates professional career showcases from multiple data sources. Parses resumes, connects to GitHub for project data, scrapes job postings, and generates brutalist-style GitHub profile READMEs and personal websites. Includes PII scanning for privacy protection.

**Stack:**
- TypeScript + Node.js
- Vitest (Testing)
- GitHub API (Project data)
- SerpAPI (Search/enrichment)
- PDF parsing (Resume extraction)

**Features:**
- Resume PDF parsing and extraction
- GitHub repository analysis
- Project abstract generation
- Brutalist design system
- PII scanning and redaction
- GitHub profile README generation
- Personal website builder
- Job posting scraper
- Knowledge base storage

**Architecture:**
```
src/
├── builders/       # Website generation
├── connectors/     # GitHub, SerpAPI integrations
├── design/         # Design system tokens
├── generators/     # Abstract & README generators
├── integrators/    # Resume parser, profile merger
├── scrapers/       # Job posting scraper
├── services/       # PII scanner
├── storage/        # Knowledge base
└── types/          # TypeScript interfaces
```

**Status:** Active Development

---

## 🛠️ Built With

All projects leverage the **$0 Vibe Coding Stack**:

| Category | Tool | Cost |
|----------|------|------|
| IDE | Google AntiGravity / Kiro | Free |
| AI Coding | Claude Code, MCP | Free tier |
| Database | Supabase | Free tier |
| Auth | Stack Auth | Free <10K |
| LLM | OpenRouter, Gemini | Free tier |
| Deployment | Vercel | Free tier |
| Analytics | PostHog, Clarity, GA | Free |

---

## Project Complexity by Level

| Project | Level | Time to MVP | Key Learning |
|---------|-------|-------------|--------------|
| Modern CV | Beginner | 2-4 hrs | API integrations |
| re:Inforce Dashboard | Intermediate | 1-2 days | AI summarization |
| FinTracker | Intermediate | 1 week | Financial APIs |
| FeastIQ | Advanced | 2 weeks | RAG, mobile |
| Security Agent | Advanced | 2 weeks | Agentic AI |
| ATLAS | Advanced | 3 weeks | Multi-system sync |
| Zombie Blaster | Advanced | 11 days | Real-time APIs |

---

*"Build it. Secure it. Tinker with it."*
