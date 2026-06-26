# Install For Codex Or Claude Code

This document is written for a user's coding agent. The user may ask Codex, Claude Code, or another local coding agent to install the Associative Incubation Harness into their own workspace.

## Installation Principle

Install locally, conservatively, and opt-in.

Do not create an always-on LLM loop by default.

## What You Are Installing

You are installing a local research harness that can:

```text
1. accept an explicitly assigned unresolved problem;
2. decompose it into a requirement graph;
3. discover local knowledge compartments;
4. run manual or budgeted heartbeat passes;
5. extract fresh context;
6. search for lateral mechanism bridges;
7. write inspectable candidate paths for user review.
```

## Where To Install

Prefer project-local installation.

Recommended:

```text
<user workspace>/.associative-incubation/
```

Also acceptable:

```text
<agent home>/associative-incubation/
```

Do not install into private data directories unless the user explicitly asks.

## Step 1 - Create Local Harness Directory

Create:

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

## Step 2 - Write Safe Default Config

Use safe defaults:

```json
{
  "enabled": false,
  "requires_user_assignment": true,
  "automatic_llm_heartbeat": false,
  "manual_run_enabled": true,
  "max_active_problems": 3,
  "max_runs_per_problem_per_day": 2,
  "max_context_chars_per_run": 12000,
  "max_candidate_reports_per_run": 3,
  "require_user_review_before_action": true,
  "redact_private_excerpts_by_default": true
}
```

## Step 3 - Discover Compartments

Inspect the user's workspace for knowledge compartments.

Possible compartments:

```text
notes
tasks
issues
docs
research
calendar exports
chat exports
email summaries
logs
financial records
health records
source code
project plans
news cache
```

Ask before enabling sensitive compartments.

Write `compartments.json`:

```json
{
  "compartments": [
    {
      "id": "compartment_notes",
      "label": "Notes",
      "path_or_source": "notes/",
      "data_types": ["note", "journal", "idea"],
      "enabled_for_incubation": true,
      "sensitive": false
    }
  ]
}
```

## Step 4 - Add Assignment Workflow

The user must explicitly assign a problem.

Accepted assignment language:

```text
incubate this problem: ...
assign background incubation: ...
start associative incubation for: ...
```

When assigned, create:

```text
.associative-incubation/active_problems/problem_<id>.json
```

Problem record:

```json
{
  "problem_id": "problem_001",
  "created_at": "ISO-8601",
  "plain_problem": "User's problem text",
  "status": "active",
  "budget": {
    "max_runs_per_day": 2,
    "max_candidate_reports_per_run": 3
  },
  "requirement_graph": {
    "nodes": [],
    "edges": []
  }
}
```

## Step 5 - Build Requirement Graph

Convert the problem into:

```text
desired transition
constraints
missing requirements
available resources
blocked resources
possible substitute paths
```

Requirement types should be generic:

```text
knowledge
tool
part
service
money
time
permission
access
skill
person
place
data
compute
attention
other
```

Do not force personal categories or fixed daemon names.

## Step 6 - Implement Manual Run First

Before scheduling anything, implement a manual run.

Manual run behavior:

```text
load active problem
load enabled compartments
sample fresh context
extract seeds
expand associations
map mechanisms
match against unsatisfied requirements
write candidate reports
```

If no implementation exists yet, use a documented prompt workflow rather than a hidden loop.

## Step 7 - Optional Heartbeat

Only add a scheduled heartbeat if the user explicitly asks.

Heartbeat must respect:

```text
max runs per day
max context chars
max candidates
quiet hours if configured
manual pause
per-problem disable
```

Every run must write a log entry.

## Step 8 - Candidate Review

Candidate paths should require user review.

Feedback values:

```text
accept
reject
interesting_later
unsafe
already_tried
needs_more_research
```

Accepted candidates can be promoted. Rejected candidates decay or are suppressed.

## Step 9 - Agent Instruction Snippet

Add an instruction like this to the local agent docs:

```text
Associative Incubation Harness:
Only run background incubation when the user explicitly assigns a problem.
Do not create automatic LLM loops by default.
Use local compartments only after consent.
Decompose assigned problems into requirement graphs.
Search fresh context for lateral mechanism bridges.
Surface candidate paths with source chains and risk scores.
Never take external action without explicit user approval.
```

## Step 10 - Verification Checklist

- [ ] Harness directory exists.
- [ ] Config defaults to disabled automatic heartbeat.
- [ ] User can assign a problem explicitly.
- [ ] Requirement graph is created.
- [ ] Compartments are listed and sensitive ones require consent.
- [ ] Manual run works before scheduled run.
- [ ] Candidate reports show source chain and matched requirement.
- [ ] Logs show when runs occurred and why.
- [ ] User can pause or delete active problems.
- [ ] No external action is taken automatically.

