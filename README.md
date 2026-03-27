# 🤖 AgentSprint — Multi-Agent Agile Sprint Simulator

> **Built by Monil Raval** — Certified SAFe 6 POPM | Product Owner | Ex-AGCO/Fendt, Bosch | MBA Germany

[![Live Demo](https://img.shields.io/badge/🚀%20Live%20Demo-Try%20AgentSprint-6366f1?style=for-the-badge)](https://monilraval.github.io/agentsprint/as_index.html)
[![Multi-Agent](https://img.shields.io/badge/Multi--Agent-6%20AI%20Agents-8b5cf6?style=for-the-badge)]()
[![Powered by Claude](https://img.shields.io/badge/Powered%20by-Claude%20Sonnet-0ea5e9?style=for-the-badge)](https://anthropic.com)
[![SAFe 6](https://img.shields.io/badge/SAFe%206-POPM%20Certified-10b981?style=for-the-badge)]()
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-f59e0b?style=for-the-badge)]()

---

## 🎯 What Is AgentSprint?

**AgentSprint** is one of the first multi-agent AI systems purpose-built for **Agile Sprint Planning**. Describe a feature or product challenge, and 6 specialised AI agents — each with their own persona, expertise, and system prompt — collaborate in real time to produce a complete, sprint-ready backlog.

**No other tool does this.** Existing AI tools for product management generate user stories in isolation. AgentSprint simulates an *entire agile team* debating, estimating, risk-scoring, and reviewing — just like a real PI Planning session.

---

## 🏗️ The 6-Agent Architecture

```
User Input
    │
    ▼
┌─────────────────────────────────────────────────┐
│           ORCHESTRATOR AGENT 🎯                  │
│   Receives input · Decomposes · Coordinates     │
└─────────────────┬───────────────────────────────┘
                  │ delegates in parallel
        ┌─────────┼─────────┐
        ▼         ▼         ▼
   ┌────────┐ ┌────────┐ ┌────────┐
   │PO Agent│ │Dev Agent│ │Risk    │
   │👤      │ │💻      │ │Agent ⚠️│
   │Stories │ │Estimates│ │Risks   │
   └────────┘ └────────┘ └────────┘
        │ sequential review
        ▼
   ┌────────────┐    ┌────────────┐
   │Scrum Master│    │ QA Agent   │
   │🔄 DoR/DoD  │    │🧪 Tests    │
   └────────────┘    └────────────┘
        │
        ▼
┌─────────────────────────────────┐
│   SYNTHESISED SPRINT BACKLOG    │
│   User Stories · Estimates ·    │
│   Risks · Tests · DoD           │
└─────────────────────────────────┘
```

| Agent | Role | Output |
|-------|------|--------|
| 🎯 **Orchestrator** | Coordinates all agents, synthesises final plan | Sprint kick-off · Final summary |
| 👤 **PO Agent** | Product Owner perspective | 4 User Stories · Acceptance Criteria · Priorities |
| 💻 **Dev Agent** | Engineering perspective | Effort estimate · Tech stack · Dependencies |
| ⚠️ **Risk Agent** | Risk management perspective | 3 Risks · Severity · Mitigations · Risk Score |
| 🔄 **Scrum Master** | Process compliance | DoR check · DoD criteria · Blockers · Readiness score |
| 🧪 **QA Agent** | Quality assurance perspective | Test scenarios · Edge cases · Exit criteria |

---

## 🚀 Live Demo

**[→ Open AgentSprint](https://monilraval.github.io/agentsprint/as_index.html)**

Try it with one of these prompts:
- *"Build a real-time PIM data quality dashboard for product managers to monitor and fix data errors across 4 global brands"*
- *"Add live charger availability and session pre-booking to a mobile app for EV drivers"*
- *"Create a fleet management portal with consolidated billing and cost centre allocation"*

---

## 💡 Why I Built This

I spent 10 months as a **Product Owner at AGCO/Fendt** running SAFe PI Planning for 4 teams across global brands. Sprint planning consumed 2–3 days per sprint. The process was:

1. Write user stories (PO)
2. Get dev estimates (Dev Team)
3. Identify risks (Risk Register)
4. Check DoR compliance (Scrum Master)
5. Write test scenarios (QA)
6. Synthesise into a sprint plan (Everyone)

AgentSprint simulates steps 1–6 in under 60 seconds.

---

## 🛠️ Technical Architecture

### Multi-Agent Orchestration Pattern

AgentSprint uses a **sequential orchestration pattern** with parallel delegation:

```javascript
// Each agent has a unique system prompt (persona)
const AGENTS = {
  orchestrator: { persona: "You are the Orchestrator Agent..." },
  po:           { persona: "You are the Product Owner Agent..." },
  dev:          { persona: "You are the Developer Agent..." },
  risk:         { persona: "You are the Risk Agent..." },
  sm:           { persona: "You are the Scrum Master Agent..." },
  qa:           { persona: "You are the QA Agent..." }
};

// Orchestration flow
async function runAgents(feature) {
  await callClaude(AGENTS.orchestrator.persona, feature);  // Kick-off
  await callClaude(AGENTS.po.persona, feature);            // User stories
  await callClaude(AGENTS.dev.persona, feature);           // Estimates
  await callClaude(AGENTS.risk.persona, feature);          // Risks
  await callClaude(AGENTS.sm.persona, feature);            // DoR/DoD
  await callClaude(AGENTS.qa.persona, feature);            // Tests
  // Synthesise → Sprint Plan
}
```

### Design Decisions

| Decision | Choice | Reason |
|----------|--------|--------|
| Framework | Vanilla JS | Zero dependencies, runs anywhere, GitHub Pages compatible |
| Agent Communication | Sequential API calls | Simpler to debug, easier to follow for demo purposes |
| Model | Claude Sonnet claude-sonnet-4-20250514 | Best balance of speed and quality for agentic tasks |
| Persistence | In-memory | No backend needed, fully client-side |

---

## 📦 Repository Structure

```
agentsprint/
├── index.html          # Complete app — single file, zero dependencies
├── README.md           # This file
├── architecture.md     # Deep dive into multi-agent design
└── examples/
    └── sample-output.md  # Example sprint plan outputs
```

---

## 🔧 Run Locally

```bash
git clone https://github.com/monilraval/agentsprint.git
cd agentsprint
open index.html  # That's it. No npm. No install. No config.
```

To enable AI generation, the app calls the Anthropic API directly from the browser. Add your API key in the fetch headers (for local testing only — never commit keys).

---

## 📊 AgentSprint vs Existing Tools

| Feature | AgentSprint | ChatGPT prompt | Jira AI | GitHub Copilot |
|---------|------------|----------------|---------|----------------|
| Multiple agent perspectives | ✅ 6 agents | ❌ Single response | ❌ | ❌ |
| Dedicated Risk Agent | ✅ | ❌ | ❌ | ❌ |
| SAFe methodology built-in | ✅ | ❌ | ❌ | ❌ |
| DoR/DoD compliance check | ✅ | ❌ | ❌ | ❌ |
| Zero dependencies | ✅ | N/A | ❌ | ❌ |
| Open source | ✅ | ❌ | ❌ | ❌ |
| Built by a real PO | ✅ | ❌ | ❌ | ❌ |

---

## 🗺️ Roadmap

- [ ] **v1.1** — Export sprint plan as JIRA-compatible CSV
- [ ] **v1.2** — Persistent sprint history across sessions
- [ ] **v1.3** — Agent memory (agents reference previous sprint decisions)
- [ ] **v2.0** — Real parallel agent execution using Web Workers
- [ ] **v2.1** — SAFe PI Planning mode (multiple teams, Program Board)

---

## 🤝 Contributing

PRs welcome. If you're a Product Owner, Scrum Master, or agile practitioner and want to improve the agent personas — open an issue or PR.

---

## 📄 License

MIT — free to use, fork, and build on.

---

## 🔗 Connect

| | |
|--|--|
| **LinkedIn** | [linkedin.com/in/monil-raval](https://linkedin.com/in/monil-raval) |
| **Website** | [clarushorizon.com](https://clarushorizon.com) |
| **Email** | monilraval@gmail.com |
| **SAFe Cert** | ID: 76253775-6778 |

---

*AgentSprint was built because the best way to demonstrate product thinking is to build the product. This is how I work: I don't just talk about agile — I ship it.*

---

⭐ **If this helped you, please star the repo — it helps other PMs find it.**
