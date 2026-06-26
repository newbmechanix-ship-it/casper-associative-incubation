# Agentic Harness Specification

## Purpose

This document defines the GitHub-safe version of the associative incubation mechanism.

It is not tied to any fixed daemon names, private stores, or personal module layout. A user's coding agent installs this harness into the user's own workspace, discovers the knowledge compartments that already exist there, and only runs background incubation when the user explicitly assigns a problem.

## Mechanism Name

**Requirement-Guided Associative Incubation**

Short form:

**Associative Incubation Harness**

## System Claim

A coding agent can improve unresolved problem solving by converting an assigned problem into a requirement graph, discovering local knowledge compartments, and periodically searching fresh context for lateral mechanism bridges that satisfy blocked requirements.

## Non-Goals

This harness is not:

- an autonomous always-on assistant;
- a generic memory scraper;
- a fixed health/work/money/social daemon layout;
- a replacement for user judgment;
- a system that takes action without review;
- a token-unbounded background loop.

## User Trigger

The harness starts only when the user explicitly assigns a problem.

Example triggers:

```text
incubate this problem: I need to fix my vehicle but lack money and tools
assign background agent: find indirect ways to get collaborator access
start associative incubation for: reduce hosting cost without hurting reliability
```

The coding agent should store an active problem only after explicit user intent.

## High-Level Loop

```text
assigned problem
  -> plain-language problem record
  -> CASCADE-style mechanism decode
  -> requirement graph
  -> local compartment discovery
  -> budgeted heartbeat passes
  -> fresh-context sampling
  -> seed extraction
  -> closest-association expansion
  -> mechanism bridge matching
  -> candidate path report
  -> user validation, rejection, promotion, or decay
```

## Dynamic Compartments

The harness should not assume fixed modules.

Instead, it discovers compartments such as:

```text
project notes
task database
issue tracker
calendar exports
email summaries
chat logs
research notes
finance logs
health logs
customer records
source code
documentation
daily journal
news cache
browser notes
```

Each compartment is described generically:

```json
{
  "id": "compartment_tasks",
  "label": "Tasks",
  "path_or_source": "tasks/",
  "data_types": ["task", "deadline", "blocker"],
  "privacy": "local",
  "enabled_for_incubation": true
}
```

The user or installing agent decides which compartments are enabled.

## Passive Lateral Sentry

The harness may also run a passive sentry over enabled compartments, but only within the user's budget and consent settings.

The sentry detects cross-compartment effects.

Generic examples:

```text
financial stress -> possible anxiety or health risk
deadline pressure -> possible communication risk
sleep disruption -> possible work quality risk
customer conflict -> possible revenue risk
tool access issue -> possible schedule slip
```

These are not hardcoded domains. They are inferred from the compartments present in the user's workspace.

The sentry should output:

```text
source compartments
detected relation
possible consequence
confidence
risk
recommended user review
```

It should not make diagnoses, financial decisions, or third-party actions.

## Requirement Graph

Every assigned problem is reduced into requirements.

Example:

```text
fix vehicle
  -> diagnose issue
     -> knowledge
     -> inspection access
  -> repair issue
     -> tools
     -> parts
     -> skill
     -> workspace
  -> outsource issue
     -> service
     -> price
     -> transportation
  -> fund issue
     -> money
     -> budget
     -> earning path
     -> cost reduction
```

Requirement node schema:

```json
{
  "id": "req_money",
  "label": "fund repair",
  "type": "money",
  "status": "unsatisfied",
  "constraints": ["low budget", "unknown repair price"],
  "candidate_paths": []
}
```

The graph should be editable by the user.

## Fresh Context Sampling

At each approved heartbeat, the harness samples enabled compartments since the last run.

It extracts:

```text
nouns
verbs
objects
places
people
skills
services
prices
events
risks
offers
constraints
opportunities
mechanisms
```

The harness is not searching only for exact problem words. It is searching for words and situations that could satisfy requirements.

## Closest-Association Expansion

Each seed can be expanded through nearby language.

Example:

```text
BBQ
  -> barbecue party
  -> prepared food
  -> informal food service
  -> paid order
  -> money
```

The association is constrained by the requirement graph:

```text
Does this chain satisfy a blocked requirement?
```

## Mechanism Bridge Test

A bridge candidate must pass three tests.

```text
semantic bridge:
  can the terms be plausibly connected?

mechanism bridge:
  does the source signal contain a mechanism that maps to the requirement?

usefulness bridge:
  does the bridge imply an actionable next step or experiment?
```

If the bridge does not improve a requirement node, it should not be surfaced.

## Candidate Output

```json
{
  "candidate_id": "bridge_001",
  "problem_id": "problem_vehicle_repair_001",
  "source_signal": {
    "compartment_id": "compartment_journal",
    "excerpt": "BBQ at dad's house was really good this week."
  },
  "seed": "BBQ",
  "association_chain": [
    "BBQ",
    "prepared food",
    "informal food service",
    "paid order",
    "money"
  ],
  "matched_requirement": "req_money",
  "candidate_path": "Evaluate whether a small BBQ plate sale or food-prep job could fund part of the repair.",
  "scores": {
    "relevance": 0.72,
    "novelty": 0.81,
    "mechanism_fit": 0.74,
    "actionability": 0.55,
    "traceability": 0.91,
    "risk": 0.38
  },
  "status": "needs_user_review"
}
```

## Budgeted Heartbeat

The harness must have a budget gate.

Recommended defaults:

```json
{
  "enabled": false,
  "requires_user_assignment": true,
  "max_active_problems": 3,
  "max_runs_per_problem_per_day": 2,
  "max_context_chars_per_run": 12000,
  "max_candidate_reports_per_run": 3,
  "run_llm_on_tick": false,
  "allow_manual_run": true
}
```

The safest default is:

```text
No automatic LLM heartbeat until the user turns it on for a specific problem.
```

## Filesystem Layout

Suggested local installation:

```text
.associative-incubation/
  config.json
  compartments.json
  active_problems/
  runs/
  candidates/
  feedback/
  logs/
```

This folder should live inside the user's agent workspace or project root unless the user chooses a global install.

## Minimal Commands

The installing coding agent can implement commands like:

```text
incubation init
incubation assign "problem text"
incubation list
incubation run --problem <id>
incubation pause --problem <id>
incubation feedback --candidate <id> --accept|--reject
```

For Codex or Claude Code, these may be scripts, tasks, slash commands, or documented workflows rather than a full CLI.

## Safety Boundary

The harness can suggest. It must not act externally without explicit user approval.

Do not automatically:

- send messages;
- spend money;
- contact third parties;
- change production systems;
- make medical, legal, or financial conclusions;
- ingest private sources without user permission.

## GitHub Positioning

This harness should be described as:

```text
experimental research scaffold
opt-in background ideation mechanism
agent-installed local workflow
```

Not as:

```text
proven benchmark winner
autonomous assistant
medical/financial advisor
token-unbounded daemon
```

