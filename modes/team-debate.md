# Mode 3: Team Debate

## When
- Context exceeds single-agent capacity (many tables, complex existing system)
- Implementation tasks can genuinely proceed in parallel
- User explicitly requests team collaboration
- Request requires reading/modifying files across 3+ distinct domain areas

## Prerequisite
The `team-workflow` skill MUST be loaded first. This file extends team-workflow with domain-specific decomposition — it does not replace it.

## Domain Extensions to team-workflow

### Task Decomposition
When decomposing the user's request into steps, assign each step a primary persona:

```
Step: "Design ingestion pipeline" → persona: data-engineer
Step: "Define feature schema" → persona: data-scientist
Step: "Apply masking policies" → persona: governance-steward
Step: "Build Streamlit dashboard" → persona: frontend-agent-dev
Step: "Author semantic model" → persona: analytics-engineer
```

### Persona Agent Configuration
When spawning explore/implement agents, include the relevant persona file content in the agent prompt:

```
prompt: |
  [Contents of personas/<name>.md]

  Your task: [step description]
  Apply your decision framework before implementing.
  Produce output following the handoff contract in templates/handoff-contract.md.
```

### Discovery Format (One Round)
Each persona agent produces ONE discovery with these fields:

```
RECOMMENDATION: [What to do, concretely]
RATIONALE: [Why, grounded in decision framework]
CONSTRAINT: [What must be true for this to work]
ASKS: [What this persona needs from other personas — specific, actionable]
```

### Synthesis Rules
- Collect all persona discoveries after ONE round
- Apply conflict resolution tree (from SKILL.md) to any tensions
- Maximum 2 rounds total. Second round ONLY if critical ASKS are unanswered
- Synthesize into implementation plan with persona assignments

### Governance Gate
Before proceeding from plan to implementation:
- IF Governance Steward participated → their constraints are mandatory
- IF PII, access, or compliance is involved and Governance was NOT consulted → halt and add governance step

## Agent Budget (within team-workflow's 45 cap)

| Phase | Agents | Persona role |
|-------|--------|--------------|
| Research | 2-3 | Explore agents with persona context |
| Persona Analysis | 3-4 | One per relevant domain |
| Planning | 1 | Synthesizer (no persona — uses all) |
| Implementation | 3-5 | Implementors with persona-specific guidance |
| Review | 1-2 | Reviewer + optional governance gate |
| **Total** | **~12-17** | Well within budget |

## Anti-Patterns to Avoid

- Do NOT spawn all 5 personas for every request. Select 3-4 most relevant.
- Do NOT allow multiple debate rounds. One round + synthesis. Max 2 if ASKS unanswered.
- Do NOT let persona agents work outside their boundaries. Enforce handoffs.
- Do NOT skip governance gate when PII/compliance is in scope.
