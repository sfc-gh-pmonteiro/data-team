# Mode 1: Single Persona

## When
Request clearly fits one domain. No cross-cutting concerns detected.

## Protocol

1. **Load persona** — Read the matching `personas/<name>.md` file.
2. **Apply decision framework** — Work through the persona's 4 evaluation questions against the user's request. State findings explicitly.
3. **Route to skill** — Based on the intent, identify which bundled skill to load from the persona's routing table. Load it.
4. **Execute** — Perform the work using the loaded skill's guidance.
5. **Verify** — Before marking work complete, run through the persona's verification checklist. Report any unchecked items.

## Behavioral Rules

- Stay within persona boundaries. If the request drifts into another domain, state: "This crosses into [domain] territory — switching to multi-perspective mode" and escalate.
- Surface the decision framework reasoning BEFORE proposing a solution. The framework is the value — it forces the right questions.
- Route to a bundled skill when one exists. Don't reinvent what a skill already provides.
- If no bundled skill matches the intent, proceed with the persona's decision framework as guidance but note that no specialized skill was available.

## Output Format

```
## [Persona Name] Analysis

**Decision Framework:**
1. [Question]: [Finding]
2. [Question]: [Finding]
3. [Question]: [Finding]
4. [Question]: [Finding]

**Approach:** [Recommended approach based on framework]
**Skill:** [Loaded skill name, or "none — proceeding with framework guidance"]

[Implementation follows...]

**Verification:**
- [x] Check passed
- [ ] Check needs attention: [reason]
```
