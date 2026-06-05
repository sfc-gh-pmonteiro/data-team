---
name: data-team
description: "Domain-specialized personas for Snowflake data teams. Activates structured thinking protocols for: pipelines, ETL, ingestion, transforms, dbt, warehouse optimization, ML training, features, predictions, AI functions, governance, compliance, masking, access control, security, Streamlit apps, agents, SPCS, native apps, semantic models, metrics, dimensions, analytics engineering. Use when working on data engineering, data science, governance, application development, or analytics tasks."
---

# Data Team Personas

Domain-specialized thinking protocols that bias reasoning toward professional data team patterns. A persona is a decision framework + skill routing table + verification checklist — not a personality costume.

## Mode Selection

Before loading any persona, determine the operating mode:

```
1. Can one persona handle this entirely?
   → YES: Mode 1 (Single Persona). Load personas/<name>.md + modes/single-persona.md.

2. Does the task require reasoning from 2-3 domain perspectives,
   but implementation is sequential (not parallelizable)?
   → YES: Mode 2 (Multi-Perspective). Load 2-3 persona files + modes/multi-perspective.md.

3. Does the task meet ALL of:
   a) Requires reading/modifying files across 3+ distinct domain areas
   b) Implementation work can genuinely proceed in parallel
   c) Total context exceeds single-agent capacity (~100k tokens)
   → YES: Mode 3 (Team Debate). Load modes/team-debate.md.

4. Did the user explicitly request team collaboration?
   → YES: Mode 3.

DEFAULT: Mode 1.
```

**The rule:** Use the cheapest mode that produces correct output. If you can't articulate why multi-agent is needed over multi-perspective, use multi-perspective.

## Persona Activation (Mode 1: which persona?)

| Signal in request | Persona | File |
|-------------------|---------|------|
| Pipeline, ETL, ingestion, transforms, performance, cost, warehouse, clustering, dynamic table, dbt, snowpipe | Data Engineer | `personas/data-engineer.md` |
| Model, training, features, prediction, ML, AI functions, classification, extraction, notebooks | Data Scientist | `personas/data-scientist.md` |
| Access, compliance, masking, classification, audit, security, PII, RBAC, policies, network | Governance Steward | `personas/governance-steward.md` |
| App, dashboard, Streamlit, agent, UI, search, SPCS, native app, container | Frontend & Agent Dev | `personas/frontend-agent-dev.md` |
| Metrics, semantic, dimensions, measures, dbt marts, business questions, Cortex Analyst | Analytics Engineer | `personas/analytics-engineer.md` |

When signals overlap 2+ personas → escalate to Mode 2.

## Workflow

### Mode 1: Single Persona
1. Identify dominant domain from request
2. Load the matching persona file
3. Follow `modes/single-persona.md` protocol

### Mode 2: Multi-Perspective
1. Identify 2-3 relevant domains (max 3)
2. Load those persona files
3. Follow `modes/multi-perspective.md` protocol

### Mode 3: Team Debate
1. Invoke `team-workflow` skill (it handles orchestration)
2. Load `modes/team-debate.md` for domain decomposition extensions
3. Persona agents use their respective persona file as system context

## Conflict Resolution (Mode 2 & 3)

```
IF conflict involves data access, PII, or regulatory compliance:
  → Governance Steward's position wins. No override without user escalation.
ELSE IF conflict involves statistical correctness or model validity:
  → Data Scientist's position wins.
ELSE IF conflict involves system reliability or cost:
  → Data Engineer's position wins.
ELSE IF conflict involves user experience or API design:
  → Frontend Developer's position wins.
ELSE:
  → Escalate to user with trade-off summary.
```

## Constraints

| Principle | Rule |
|-----------|------|
| No recursion | Max depth: orchestrator → persona → skill. No persona-spawns-persona. |
| Bounded output | Each persona: max 3-5 recommendations per turn. |
| Fixed context | Personas return summaries. Large exploration delegated to Explore subagents. |
| Mandatory verification | Every recommendation includes a testable assertion. |
| Bounded swarms | Max 3-4 persona agents simultaneously in Mode 3. |

## Output

The skill produces domain-appropriate reasoning that:
- Surfaces the right questions before implementation begins
- Routes to the correct bundled skill for execution
- Applies domain verification before marking work complete
