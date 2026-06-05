# Handoff Contract Template

Inter-persona output contract for Mode 3 (Team Debate). Each persona agent producing work that another persona will consume MUST declare this contract.

## Contract Fields

```yaml
producer: <persona-name>
consumer: <persona-name or "any">
artifact:
  type: <table | view | function | model | app | config | document>
  name: <fully-qualified object name or file path>
  grain: <what one row represents>
  freshness: <max acceptable lag, e.g. "15 minutes", "daily", "real-time">
  schema:
    - column: <name>
      type: <snowflake type>
      description: <what it means>
      sensitive: <true | false>
constraints:
  - <constraint 1, e.g. "Must be idempotent on re-run">
  - <constraint 2, e.g. "PII columns must be masked before consumer access">
downstream_consumers:
  - <who reads this: persona name + purpose>
```

## Example

```yaml
producer: data-engineer
consumer: analytics-engineer
artifact:
  type: dynamic table
  name: ANALYTICS.SILVER.FCT_USER_SESSIONS
  grain: one row per user session
  freshness: "15 minutes (target_lag)"
  schema:
    - column: SESSION_ID
      type: VARCHAR
      description: Unique session identifier
      sensitive: false
    - column: USER_ID
      type: VARCHAR
      description: Anonymized user identifier
      sensitive: true
constraints:
  - Idempotent refresh (Dynamic Table handles this)
  - USER_ID tokenized before Silver layer (governance requirement)
downstream_consumers:
  - analytics-engineer: semantic model for session metrics
  - data-scientist: feature input for churn model
```

## Usage

- Producers declare contracts BEFORE implementation begins
- Consumers validate contracts match their requirements
- Governance Steward reviews contracts containing `sensitive: true` fields
- Contract mismatches are resolved via conflict resolution tree in SKILL.md
