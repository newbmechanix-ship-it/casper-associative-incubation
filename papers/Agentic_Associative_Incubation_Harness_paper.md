# Agentic Associative Incubation Harness
### An opt-in background problem-solving capability for coding agents

**Author:** Spectromachina  
**Status:** GitHub-facing system proposal / experimental harness  
**Companion theory papers:** `Associative_Retrieval_research_note.md`, `CASPER_Longitudinal_Keyword_Pathways_paper.md`, `CASPER_Requirement_Guided_Associative_Incubation_paper.md`

---

## Abstract

This paper proposes an installable **Agentic Associative Incubation Harness** for coding agents such as Codex or Claude Code. The harness gives an agent an opt-in background problem-solving capability: when a user explicitly assigns an unresolved problem, the agent converts it into a requirement graph, expands that graph into many possible solution branches, discovers the user's local knowledge compartments, and performs budgeted incubation passes that search memory and fresh context for lateral mechanism bridges.

The mechanism is experimental and must not run as an unbounded background LLM loop. The default installation is manual and disabled until the user assigns a problem. Once assigned, the harness can periodically inspect enabled compartments such as notes, tasks, research files, project logs, issue trackers, or other user-approved sources. It extracts words and events, expands them through close lexical associations, infers mechanisms, and tests whether any mechanism can satisfy a blocked requirement.

The contribution is not generic task decomposition, memory, or random-word creativity. The contribution is an agent-installable loop:

```text
voluntary problem assignment
  -> requirement graph
  -> explosive branch expansion
  -> dynamic compartment discovery
  -> budgeted heartbeat pass
  -> memory probes / public probes / lateral association
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

## 8. Explosive Requirement Branching

The requirement graph is not a flat checklist. It is a root system.

The root is the assigned problem:

```text
reduce cloud hosting cost without hurting reliability
```

The first expansion produces requirements:

```text
lower recurring cost
preserve uptime
preserve performance
identify cost drivers
reduce repeated work
reduce storage cost
reduce egress
avoid risky architecture changes
```

Each requirement can then branch into possible mechanisms:

```text
lower recurring cost
  -> remove idle resources
  -> cache repeated work
  -> compress stored assets
  -> move cold data
  -> reduce egress
  -> change pricing tier
  -> request credits
  -> replace expensive dependency
```

This behavior can feel like roots expanding quickly into thousands of paths. The harness should support that expansion, but it must also prune aggressively. Branching is useful only when constrained by the root problem, user consent, source availability, cost, risk, and token budget.

Branch expansion operators:

```text
requirement decomposition
memory entity probe
second-degree relationship probe
affiliation probe
public channel probe
program/opportunity probe
event/location probe
cost-reduction probe
substitution probe
constraint bypass probe
lateral analogy probe
```

The harness should surface only the strongest candidate paths, not the entire branch tree.

## 9. Search Modes

The harness has three complementary search modes.

```text
1. Context-driven bridge search
   fresh daily signal -> association -> requirement match

2. Requirement-driven memory probe
   unsatisfied requirement -> memory entities -> possible satisfiers

3. Passive cross-compartment sentry
   one compartment signal -> possible effect in another compartment
```

The BBQ example is context-driven. A cloud-cost example is requirement-driven.

Requirement-driven memory probe:

```text
problem:
  reduce cloud hosting cost without hurting reliability

requirement:
  lower recurring cost while preserving uptime and performance

branch:
  caching / storage tiering / idle cleanup

memory probe:
  logs, docs, billing notes, and code references
  -> repeated thumbnail generation
  -> compute and storage cost pattern

candidate bridge:
  repeated thumbnail generation -> wasted compute -> caching branch -> lower cost
```

This is not merely association from a random word. It is a directed search from an unsatisfied requirement into memory.

## 10. Heartbeat Incubation Pass

A heartbeat pass is a budgeted check.

```text
load active assigned problems
load requirement graphs
expand or refresh candidate branches
load enabled compartments
sample changed context and relevant memory
extract seeds
probe memory entities, assets, files, logs, channels, and close associations
infer mechanisms
match mechanisms to unsatisfied requirements
score candidate bridges
write candidate reports
```

The pass can be manual or scheduled. Manual comes first.

## 11. Lateral Mechanism Bridge

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

## 12. Cost Reduction Branch Example

The same mechanism can search for technical cost paths rather than money-generation paths.

Example:

```text
assigned problem:
  reduce hosting cost without reducing reliability

requirement:
  lower recurring cost while preserving uptime and performance

branch expansion:
  cache repeated work
  reduce storage
  move cold data
  remove idle resources
  change pricing model

memory probe:
  logs mention repeated thumbnail generation
  billing notes mention compute/storage increase
  code references image processing

candidate path:
  cache generated thumbnails and move originals to cold storage
```

The point is not that the branch list is predefined. The agent builds the branch tree from the problem, probes memory for clues, prunes weak branches, and surfaces only candidate paths that can state their functional mechanism.

## 13. Candidate Path Format

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

Cost candidate:

```json
{
  "candidate_id": "bridge_cost_001",
  "problem_id": "problem_hosting_cost_001",
  "source_signal": {
    "compartment_id": "compartment_logs",
    "excerpt": "Repeated thumbnail generation appears in recent processing logs."
  },
  "branch_operator": "cost_reduction_probe",
  "association_chain": [
    "repeated thumbnail generation",
    "wasted compute",
    "cache generated thumbnails",
    "lower recurring cost"
  ],
  "matched_requirement": "req_lower_cost",
  "candidate_path": "Evaluate caching generated thumbnails and moving originals to cheaper storage.",
  "status": "needs_user_review"
}
```

## 14. Feedback Loop

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

## 15. Installation Model

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
Expand requirement branches under a budget.
Search fresh context and memory for mechanism bridges.
Surface candidate paths with source chains and risk scores.
Never take external action without approval.
```

## 16. Evaluation Plan

Compare:

```text
A. direct prompt only
B. direct prompt plus task decomposition
C. random-word association
D. requirement graph only
E. requirement graph plus compartment retrieval
F. requirement graph plus branch expansion
G. full heartbeat incubation with bridge scoring
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
G vs B:
  does incubation beat decomposition?

G vs C:
  does requirement filtering beat random association?

G vs F:
  does repeated context/memory probing improve over one-shot branch expansion?

G token cost:
  can this run within an acceptable user budget?
```

## 17. Safety Limits

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

## 18. Conclusion

The Agentic Associative Incubation Harness proposes an opt-in capability for coding agents:

```text
assigned problem
  -> requirement graph
  -> branch expansion
  -> dynamic compartments
  -> budgeted heartbeat
  -> memory/public/lateral mechanism bridge
  -> inspectable candidate path
```

This turns an agent from a foreground-only responder into a controlled background incubator, without requiring fixed modules or unbounded token spending.

The research question is:

> Can voluntary, budgeted background incubation over local knowledge compartments and rapidly expanded requirement branches surface useful non-obvious solution paths that direct prompting and ordinary task decomposition miss?
