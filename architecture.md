# AgentSprint — Multi-Agent Architecture Deep Dive

## Why Multi-Agent for Sprint Planning?

Single LLM prompts for sprint planning fail because they collapse multiple perspectives into one voice. A Product Owner, Developer, QA Engineer, Scrum Master, and Risk Manager have fundamentally different mental models — and those tensions between perspectives are what produces good sprint plans.

By giving each role a dedicated system prompt (agent persona), we force the model to:
1. Commit to a specific perspective before generating output
2. Produce outputs in the format that role would naturally use
3. Create constructive tension between agents (dev estimates vs PO story count)

## Agent Persona Design

Each agent persona is engineered with three components:

**Role declaration** — "You are the [Role] Agent in an agile sprint simulation"
**Output specification** — Exact format, length, and structure required
**Constraint** — What the agent should NOT do (e.g., Risk Agent doesn't write user stories)

This mirrors the **Constitutional AI** approach — giving agents explicit principles to follow.

## Orchestration Pattern

AgentSprint uses **Sequential Orchestration with Parallel Delegation** — a pattern where:

1. The Orchestrator sets context and frames the problem
2. Specialist agents run in sequence (not parallel) for clarity and debuggability  
3. The Orchestrator synthesises all outputs

**Why sequential vs parallel?**
Parallel would be faster but creates coordination complexity. For a demo/portfolio tool, sequential execution makes the agent thinking visible step-by-step — which is pedagogically valuable and more engaging for users watching the agents activate in order.

In production (v2.0 roadmap), Web Workers would enable true parallel execution.

## System Prompt Engineering

The key insight: **output format specification in the system prompt dramatically improves parsing reliability**.

Bad persona: "Write user stories for this feature."
Good persona: "Write exactly 4 user stories in this format: **US-001 | [Title]** / As a [persona] I want [action] so that [benefit]. / Priority: P1/P2/P3 | Points: X"

The structured output spec allows client-side parsing without a backend.

## Extensibility

To add a new agent:
1. Add entry to `AGENTS` object with `name`, `color`, `avatar`, `badge`, `persona`
2. Add agent card HTML to sidebar
3. Add `callClaude(AGENTS.newAgent.persona, context)` step in `runAgents()`
4. Optionally add a parser for structured output (like `parseAndRenderStories`)

The architecture is deliberately simple to encourage contribution and extension.

---

*Written by Monil Raval — Product Owner, SAFe 6 POPM*
