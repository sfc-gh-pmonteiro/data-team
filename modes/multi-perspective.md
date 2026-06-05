# Mode 2: Multi-Perspective Analysis

## When
Request crosses 2-3 domains but one agent can reason through all perspectives sequentially. Total context fits in a single agent's window.

## Why This Over Mode 3
Same quality output. 75% fewer tokens. Zero coordination overhead. No message-passing latency. Prompting one agent to consider multiple perspectives sequentially is functionally equivalent to multiple agents producing discoveries — minus the serialization cost.

## Protocol

1. **Identify perspectives** — Select 2-3 relevant personas (max 3, diminishing returns past that).
2. **Load persona files** — Read each selected `personas/<name>.md`.
3. **Sequential reasoning** — For each persona, apply its decision framework to the request. Produce a typed analysis block.
4. **Synthesize** — After all perspectives complete, identify:
   - Points of agreement (proceed with these)
   - Points of tension (apply conflict resolution from SKILL.md)
   - Gaps no persona covered (flag for user)
5. **Route to skills** — Load the primary skill needed for implementation. Secondary skills loaded as needed during execution.
6. **Verify** — Apply verification checklists from ALL loaded personas.

## Behavioral Rules

- Do NOT load more than 3 perspectives. If you think you need 4+, escalate to Mode 3.
- Keep each perspective's analysis to 3-5 sentences. This is not a debate — it's structured consideration.
- Apply conflict resolution immediately — don't present unresolved tensions to the user unless the conflict tree says "Escalate."
- The synthesis produces ONE coherent recommendation, not a menu of options.

## Output Format

```
## Multi-Perspective Analysis

### [Persona 1] Perspective
**Framework evaluation:** [2-3 key findings from this persona's 4 questions]
**Recommendation:** [What this persona would do]
**Constraint:** [What this persona would block or require]

### [Persona 2] Perspective
**Framework evaluation:** [2-3 key findings]
**Recommendation:** [What this persona would do]
**Constraint:** [What this persona would block or require]

### [Persona 3] Perspective (if applicable)
[Same structure]

---

### Synthesis
**Agreement:** [Points all perspectives align on]
**Resolved tension:** [Conflict + which persona's position won + why (per resolution tree)]
**Approach:** [Unified recommendation]
**Skills loaded:** [skill-1, skill-2]

[Implementation follows...]

### Unified Verification
- [x/  ] [Checks from all relevant personas]
```
