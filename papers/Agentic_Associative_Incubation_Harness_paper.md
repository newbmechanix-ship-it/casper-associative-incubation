# Agentic Associative Incubation Harness
### An opt-in background problem-solving capability for coding agents

**Author:** Spectromachina  
**Status:** GitHub-facing system proposal / experimental harness  
**Companion theory papers:** `Associative_Retrieval_research_note.md`, `CASPER_Longitudinal_Keyword_Pathways_paper.md`, `CASPER_Requirement_Guided_Associative_Incubation_paper.md`

---

## Abstract

This paper proposes an installable **Agentic Associative Incubation Harness** for coding agents such as Codex or Claude Code. The harness gives an agent an opt-in background problem-solving capability: when a user explicitly assigns an unresolved problem, the agent converts it into a requirement graph, discovers the user's local knowledge compartments, and performs budgeted incubation passes that search fresh context for lateral mechanism bridges.

The mechanism is experimental and must not run as an unbounded background LLM loop. The default installation is manual and disabled until the user assigns a problem. Once assigned, the harness can periodically inspect enabled compartments such as notes, tasks, research files, project logs, issue trackers, or other user-approved sources. It extracts words and events, expands them through close lexical associations, infers mechanisms, and tests whether any mechanism can satisfy a blocked requirement.

The contribution is not generic task decomposition, memory, or random-word creativity. The contribution is an agent-installable loop:

```text
voluntary problem assignment
  -> requirement graph
  -> dynamic compartment discovery
  -> budgeted heartbeat pass
  -> lateral association
  -> mechanism bridge
  -> inspectable candidate path
  -> user feedback
```

---

## 1. Motivation

Coding agents are increasingly used as local collaborators. They can inspect files, modify projects, run tools, and reason over workspace state. But most agent interactions remain foreground-bound: the user asks, the agent answers, and the problem ends unless the user restarts it.

Some problems do not resolve in one interaction. They require missing resources, new context, indirect opportunities, or cross-domain effects.

Examples:

```text
need money to solve a repair problem
need a collaborator but do not know who
need tool access but do not know where
need to reduce a project cost without weakening reliability
need to notice when stress in one domain affects another domain
```

The proposed harness lets a user voluntarily assign such a problem to a local agent for background incubation.

## 2. Design Constraint: No Token Burn By Default

The harness exists because background thinking can become expensive.

Therefore:

```text
automatic LLM heartbeat: off by default
problem assignment: explicit only
scheduled runs: opt-in per problem
run budgets: required
candidate count: limited
source chains: required
external actions: forbidden without confirmation
```

This is not an always-on assistant. It is a budgeted experimental capability.

## 3. Three Theory Layers

The harness integrates three theory layers.

| Theory Paper | Role | Core Claim |
|---|---|---|
| `Associative_Retrieval_research_note.md` | associative retrieval | curated associative context may push LLMs toward useful non-obvious bridges |
| `CASPER_Longitudinal_Keyword_Pathways_paper.md` | time-indexed memory | repeated keywords and tags over time can become retrieval pathways |
| `CASPER_Requirement_Guided_Associative_Incubation_paper.md` | problem incubation | unresolved problems can be decomposed into requirement graphs and searched against future context |

The harness is the applied layer:

```text
install into agent workspace
discover local compartments
run only after user assignment
surface candidate bridges
```

## 4. Dynamic Compartments Instead Of Fixed Modules

This GitHub version does not assume fixed modules or personal daemon names.

Each user's agent workspace may have different compartments:

```text
notes
tasks
issue tracker
source code
calendar exports
email summaries
chat summaries
project logs
research notes
finance records
health records
customer records
documentation
news cache
```

The harness discovers and describes compartments generically:

```json
{
  "id": "compartment_tasks",
  "label": "Tasks",
  "path_or_source": "tasks/",
  "data_types": ["task", "deadline", "blocker"],
  "enabled_for_incubation": true,
  "sensitive": false
}
```

Sensitive compartments require explicit user consent.

## 5. Passive Lateral Sentry

The same harness can operate as a passive lateral sentry when allowed by the user.

The sentry watches enabled compartments for cross-compartment effects:

```text
budget pressure -> possible attention or wellbeing risk
deadline pressure -> possible communication risk
customer conflict -> possible revenue risk
missing tool -> possible project delay
sleep disruption -> possible work quality risk
```

These are examples, not fixed categories. The compartments are discovered from the user's own system.

The sentry should output cautious flags:

```text
source compartments
observed relation
possible consequence
confidence
risk
suggested review
```

It should not diagnose, decide, or act.

## 6. Assignment Trigger

The user must explicitly assign a problem.

Examples:

```text
incubate this problem: I need to fix my vehicle but lack money and tools
assign background incubation: find indirect ways to get a collaborator
start associative incubation for: reduce hosting cost without losing reliability
```

The trigger creates an active problem record:

```json
{
  "problem_id": "problem_001",
  "plain_problem": "I need to fix my vehicle but lack money and tools.",
  "status": "active",
  "budget": {
    "max_runs_per_day": 2,
    "max_candidate_reports_per_run": 3
  }
}
```

## 7. Requirement Graph

The agent converts the assigned problem into a requirement graph.

Generic requirement types:

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

Example:

```text
fix vehicle
  -> diagnose
     -> knowledge
     -> inspection access
  -> repair
     -> tools
     -> parts
     -> skill
  -> outsource
     -> service
     -> price
  -> fund
     -> money
     -> budget
     -> earning path
```

The graph is the filter. It prevents random association from becoming noise.

## 8. Heartbeat Incubation Pass

A heartbeat pass is a budgeted check.

```text
load active assigned problems
load requirement graphs
load enabled compartments
sample changed context
extract seeds
expand seeds into close associations
infer mechanisms
match mechanisms to unsatisfied requirements
score candidate bridges
write candidate reports
```

The pass can be manual or scheduled. Manual comes first.

## 9. Lateral Mechanism Bridge

The harness searches for functional bridges, not topical matches.

Example:

```text
assigned problem:
  need money to fix vehicle

fresh context:
  "The BBQ at dad's house was good."

association:
  BBQ -> prepared food -> paid food service -> money

matched requirement:
  money

candidate path:
  evaluate whether a small food-prep sale could fund part of the repair
```

The insight is:

```text
BBQ is not about vehicles.
BBQ contains a mechanism that may satisfy a repair requirement.
```

## 10. Candidate Path Format

Every candidate must be inspectable.

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
    "paid service",
    "money"
  ],
  "matched_requirement": "req_money",
  "candidate_path": "Evaluate whether a small BBQ plate sale could fund part of the repair.",
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

## 11. Feedback Loop

The user can mark candidates:

```text
accept
reject
interesting_later
unsafe
already_tried
needs_more_research
```

Accepted bridges can be promoted. Rejected bridges decay. Unsafe classes can be blocked.

## 12. Installation Model

The harness is designed to be installed by a coding agent.

Recommended local layout:

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

The installing agent should add local instructions:

```text
Only run incubation after explicit user assignment.
Do not create automatic LLM loops by default.
Use local compartments only after consent.
Decompose problems into requirement graphs.
Search fresh context for mechanism bridges.
Surface candidate paths with source chains and risk scores.
Never take external action without approval.
```

## 13. Evaluation Plan

Compare:

```text
A. direct prompt only
B. direct prompt plus task decomposition
C. random-word association
D. requirement graph only
E. requirement graph plus compartment retrieval
F. full heartbeat incubation with bridge scoring
```

Metrics:

```text
usefulness
novelty
requirement fit
actionability
traceability
false-bridge rate
risk awareness
token cost
```

The important comparisons:

```text
F vs B:
  does incubation beat decomposition?

F vs C:
  does requirement filtering beat random association?

F token cost:
  can this run within an acceptable user budget?
```

## 14. Safety Limits

The harness may suggest but must not act.

Do not automatically:

```text
send messages
contact people
spend money
post online
change production systems
use credentials
make medical, legal, or financial conclusions
```

The system should describe risk and uncertainty. Low-confidence paths are experiments, not recommendations.

## 15. Conclusion

The Agentic Associative Incubation Harness proposes an opt-in capability for coding agents:

```text
assigned problem
  -> requirement graph
  -> dynamic compartments
  -> budgeted heartbeat
  -> lateral mechanism bridge
  -> inspectable candidate path
```

This turns an agent from a foreground-only responder into a controlled background incubator, without requiring fixed modules or unbounded token spending.

The research question is:

> Can voluntary, budgeted background incubation over local knowledge compartments surface useful non-obvious solution paths that direct prompting and ordinary task decomposition miss?

