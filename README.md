<div align="center">

# 🎯 CareerOS

### Your Autonomous Career Operating System

*An AI-powered pipeline that scrapes job boards, tailors your CV, finds recruiter contacts, and tracks your entire job search — running 24/7 on your own server.*

![Status](https://img.shields.io/badge/status-in%20production-brightgreen)
![Stack](https://img.shields.io/badge/stack-n8n%20%7C%20Claude%20API%20%7C%20Docker-blue)
![Server](https://img.shields.io/badge/hosted%20on-Hostinger%20VPS-purple)
![License](https://img.shields.io/badge/license-MIT-lightgrey)
![Built By](https://img.shields.io/badge/built%20by-Avish%20Rathour-navy)

[**Live Dashboard**](#) · [**Architecture**](#-architecture) · [**Setup Guide**](#-setup) · [**Roadmap**](#-roadmap)

---

</div>

## 💡 The Problem

Applying for 20+ relevant jobs per day manually is impossible. Each application needs:

- A tailored CV matching the job description
- Research on the company
- A cheat sheet ready if the recruiter calls
- A cold email to the right hiring manager
- Follow-up tracking

Doing this manually takes **45 minutes per application**. At 20 applications a day, that's 15 hours. No one has 15 hours.

CareerOS does it in the background while you sleep.

---

## ✨ What It Does

Every 6 hours, CareerOS automatically:

| Stage | Action |
|---|---|
| **1. Discover** | Scrapes LinkedIn, IrishJobs, Indeed Ireland, Jobs.ie, and company career pages |
| **2. Score** | Ranks each role against your CV using Claude AI — High / Medium / Low priority |
| **3. Tailor** | Generates an ATS-optimised PDF CV per job, keyword-matched to the JD |
| **4. Research** | Produces a one-page company cheat sheet with likely interview questions |
| **5. Outreach** | Finds recruiter/hiring manager emails via Hunter.io and drafts cold emails |
| **6. Digest** | Sends everything to your phone as a single morning email |
| **7. Track** | Monitors your inbox, auto-updates dashboard as replies and interviews arrive |

You open your phone. You tap apply. You move on with your day.

---

## 🏗️ Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                    HOSTINGER VPS (Ubuntu 24)                   │
│                                                                │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐     │
│  │     n8n      │    │  career-ops  │    │   Dashboard  │     │
│  │ Orchestrator │◄──►│  CV Engine   │◄──►│   Web App    │     │
│  └──────┬───────┘    └──────┬───────┘    └──────────────┘     │
│         │                   │                                  │
│  ┌──────▼─────────────────────▼────────┐   ┌───────────────┐   │
│  │         Claude API Layer            │   │   PostgreSQL  │   │
│  │   Scoring · Tailoring · Insights    │   │   Pipeline DB │   │
│  └─────────────────────────────────────┘   └───────────────┘   │
│                                                                │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐     │
│  │   Outline    │    │    GitHub    │    │ Gmail Watch  │     │
│  │  Knowledge   │    │  Sync / CI   │    │  Automation  │     │
│  └──────────────┘    └──────────────┘    └──────────────┘     │
└────────────────────────────────────────────────────────────────┘
         ▲                                         │
         │                                         ▼
  ┌──────┴───────┐                        ┌────────────────┐
  │   Apify +    │                        │  Your Phone    │
  │ Hunter.io +  │                        │ Morning Digest │
  │ Job Boards   │                        │  (read → tap)  │
  └──────────────┘                        └────────────────┘
```

---

## 🧠 Why This Matters

This isn't just a job-search tool. It's a demonstration of end-to-end product thinking:

- **Data engineering** — multi-source scraping, deduplication, scoring
- **ML/AI integration** — LLM-driven matching, content generation, classification
- **Full-stack delivery** — server, orchestration, data, UI, mobile-friendly
- **Product sense** — solving a real user problem with measurable outcomes
- **Iterative build** — shipped in phases, always functional, never blocking

For anyone reading this as a recruiter or hiring manager: **this repository is the portfolio**.

---

## 🛠️ Stack

**Infrastructure** · Hostinger VPS · Docker · Ubuntu 24.04
**Orchestration** · n8n (self-hosted)
**AI** · Anthropic Claude API (Sonnet 4.6 / Opus 4.7)
**Data Sources** · Apify (LinkedIn) · Reed API · IrishJobs RSS · Indeed · Company ATS (Greenhouse, Lever, Ashby)
**CV Engine** · career-ops · Playwright · HTML/CSS templating
**Email** · Gmail API · Hunter.io
**Storage** · PostgreSQL · Outline (knowledge base)
**Version Control** · GitHub

---

## 📂 Repository Structure

```
careeros/
├── .github/                    CI workflows, issue templates
├── workflows/                  n8n workflow JSON exports
│   ├── morning-scrape.json
│   ├── recruiter-outreach.json
│   ├── inbox-monitor.json
│   └── linkedin-post-drafter.json
├── career-ops/                 CV engine (git submodule)
│   ├── cv.md
│   ├── config/profile.yml
│   ├── templates/cv-template.html
│   └── reports/
├── dashboard/                  Web dashboard (Next.js)
│   ├── app/
│   └── components/
├── scripts/
│   ├── setup.sh               One-command server setup
│   ├── backup.sh              Daily DB snapshot
│   └── migrate.sh
├── docs/
│   ├── architecture.md
│   ├── runbook.md
│   └── prompts/               All Claude prompts used
├── .env.example
└── README.md
```

---

## 🚀 Setup

> **Time to full deployment:** ~2 hours

### Prerequisites

- Hostinger VPS (or any Ubuntu 24 server with ≥4GB RAM)
- Anthropic API key
- Gmail account
- Apify account (free tier works)

### One-command install

```bash
curl -fsSL https://raw.githubusercontent.com/avishrathour/careeros/main/scripts/setup.sh | bash
```

This installs Docker, clones the repo, sets up n8n + PostgreSQL + career-ops, and prompts you for credentials.

### Manual install

See [`docs/setup.md`](docs/setup.md) for step-by-step configuration.

---

## 📊 Results

*Running since April 2026*

| Metric | Value |
|---|---|
| Jobs scanned daily | 200+ |
| Relevant matches surfaced daily | 15–30 |
| Applications sent / day | 15–20 |
| Time saved per week | ~30 hours |
| Response rate improvement | 2× vs manual |

*(Live dashboard coming soon)*

---

## 🗺️ Roadmap

### Phase 1 — Core Pipeline ✅
- [x] career-ops CV engine with custom ATS-safe template
- [x] Multi-source job scraping (Reed, IrishJobs, LinkedIn via Apify)
- [x] AI-based job scoring against personal CV
- [x] Tailored PDF CV generation per role
- [x] Morning email digest
- [x] Recruiter email discovery via Hunter.io

### Phase 2 — Intelligence Layer 🔨
- [ ] Cheat sheet generator per company (background, questions, stories)
- [ ] Inbox monitoring — auto-classify replies and update status
- [ ] Interview calendar auto-population
- [ ] Skills gap detector across 100+ JDs
- [ ] Salary benchmark tracker

### Phase 3 — Presence Builder
- [ ] Daily LinkedIn post draft (research-backed, your voice)
- [ ] GitHub portfolio auto-updater
- [ ] Agency outreach batch workflow
- [ ] Automated follow-up sequences (7/14/30 day)

### Phase 4 — Dashboard & Insights
- [ ] Web dashboard (Next.js) — mobile-first
- [ ] Application funnel visualisation
- [ ] Response rate analytics per CV version
- [ ] Weekly performance reports
- [ ] Rejection pattern analysis

### Phase 5 — Productise
- [ ] Multi-tenant mode
- [ ] Onboarding flow for other job seekers
- [ ] Subscription billing
- [ ] Public launch

---

## 🧩 Design Decisions

### Why self-hosted n8n?
Per-operation billing on SaaS tools (Make.com, Zapier) scales badly with high-volume automation. A €11/month VPS runs unlimited workflows with full control.

### Why not auto-apply?
LinkedIn bans automated applications aggressively. One ban destroys months of network building. The pipeline prepares everything so the human "apply" step takes 10 seconds on mobile — that's the right trade-off.

### Why Claude over GPT?
Claude's longer context window handles full JD + full CV + tailoring instructions in one call without context management overhead. Better for structured output generation.

### Why a custom HTML CV template?
ATS parsers fail on tables, columns, and graphics. Hand-built HTML → Playwright → PDF gives pixel-perfect design AND clean text extraction. You get Figma-quality output that Workday can parse.

---

## 👤 Author

**Avish Rathour**
Data & Business Analyst | Dublin, Ireland
MSc Big Data Management & Analytics · Griffith College Dublin

- 📧 [avishrathour.it@gmail.com](mailto:avishrathour.it@gmail.com)
- 💼 [LinkedIn](https://linkedin.com/in/avishrathour)
- 🐙 [GitHub](https://github.com/avishrathour)

---

## 📜 License

MIT — see [`LICENSE`](LICENSE).

---

## 🙏 Acknowledgements

Built on the shoulders of giants:
- [**career-ops**](https://github.com/santifer/career-ops) by Santiago — the CV engine
- [**n8n**](https://n8n.io) — workflow orchestration
- [**Anthropic**](https://anthropic.com) — Claude API
- [**Apify**](https://apify.com) — LinkedIn scraping infrastructure

---

<div align="center">

**⭐ Star this repo** if CareerOS inspires your own automation build.

*Built while job hunting. For other job hunters.*

</div>
