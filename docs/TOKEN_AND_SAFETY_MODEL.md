# Token And Safety Model

## Why This Exists

Associative incubation can become expensive if implemented as an always-on LLM loop. The harness must be designed so users do not accidentally burn tokens.

The safe design is voluntary assignment plus explicit budget.

## Default Policy

```text
automatic background LLM calls: off
manual run: allowed
scheduled run: opt-in per problem
maximum active problems: small
maximum runs per day: small
candidate reports per run: small
```

## Recommended Budget Fields

```json
{
  "max_active_problems": 3,
  "max_runs_per_problem_per_day": 2,
  "max_context_chars_per_run": 12000,
  "max_llm_calls_per_run": 3,
  "max_candidate_reports_per_run": 3,
  "pause_after_days_without_feedback": 7
}
```

## Cheap First Pass

The harness should do cheap filtering before any LLM call.

Cheap pass:

```text
read changed files or records
extract candidate terms
filter by enabled compartments
filter by active problem requirement types
deduplicate seeds
limit context size
```

Only then should an LLM be asked to expand and judge bridges.

## Manual Run Prompt

A manual run can use this prompt pattern:

```text
Given this unresolved problem and requirement graph,
inspect the provided fresh context.
Extract only signals that could satisfy unsatisfied requirements.
For each candidate, provide:
source excerpt, seed, association chain, matched requirement,
candidate path, actionability, risk, and uncertainty.
Return at most 3 candidates.
```

## Stop Conditions

Pause incubation when:

```text
user pauses it
problem is solved
budget is exhausted
no user feedback after configured period
candidate quality is repeatedly low
source compartments become unavailable
```

## Privacy Rules

- Keep local stores local.
- Redact sensitive source excerpts by default.
- Do not ingest new private data sources without consent.
- Do not commit local harness runtime data to public GitHub.
- Provide `.gitignore` entries for `.associative-incubation/runs/`, `candidates/`, `feedback/`, and logs.

## Action Safety

The harness may propose paths. It must not act externally.

Require explicit confirmation before:

```text
sending messages
contacting people
spending money
posting online
changing production systems
using credentials
making health, legal, or financial decisions
```

## Risk Scoring

Every candidate should include risk.

Risk includes:

```text
privacy risk
money risk
social risk
health risk
legal risk
reputational risk
time cost
opportunity cost
```

Low-confidence bridges should be marked as experiments, not recommendations.

