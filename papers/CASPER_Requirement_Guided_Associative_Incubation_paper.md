# Requirement-Guided Associative Incubation
### A heartbeat agent for converting daily context into solution paths for unresolved problems

**Author:** Spectromachina | **Project:** CASPER-in-Hermes  
**Status:** Working paper / mechanism isolation  
**Related drafts:** `CASPER_Background_Mechanism_Incubation_paper.md`, `CASPER_Longitudinal_Keyword_Pathways_paper.md`, `Associative_Retrieval_research_note.md`

---

## Abstract

This paper isolates a CASPER mechanism for solving unresolved problems through background associative search. When a user presents a problem that a foreground LLM cannot solve directly, the system converts the problem into a requirement graph. Each node represents something the solution may need: knowledge, tools, parts, service, money, time, permission, access, skill, or cooperation. The graph then branches into acquisition questions: where can this requirement be found, how can it be obtained, what does it cost, what substitutes exist, and what can be done if the obvious path is unavailable?

A background heartbeat agent keeps this requirement graph active. At each interval, it reads fresh user context, messages, notes, project traces, news, and other available signal. It extracts words and situations from that signal, expands them through close lexical and semantic associations, infers their underlying mechanisms, and tests whether any of them can satisfy an unresolved branch of the graph. A casual mention of barbecue, for example, is not relevant to vehicle repair by topic. But it may be relevant by mechanism: barbecue can become a service, a service can be sold, selling produces money, and money satisfies a blocked repair requirement.

The proposed contribution is **requirement-guided associative incubation**: a persistent agent that turns unsolved problems into branching requirement graphs, then opportunistically searches daily language and world signal for mechanism bridges into those branches. The output is not a final answer, but an inspectable candidate path: source signal, association chain, matched requirement, proposed action, and confidence.

---

## 1. Motivation

Direct LLM problem solving often fails in a predictable way. The model receives a problem, reasons over the visible prompt, and returns the most literal plan it can infer. If the required solution depends on missing resources, hidden constraints, indirect opportunities, or future context, the model may have nothing useful to say.

Example:

```text
Problem:
  I need to fix a vehicle.
```

A direct answer may list generic repair steps. But the real problem may not be "how to repair a vehicle" in the abstract. It may be one or more missing requirements:

```text
knowledge
tools
parts
service
money
time
transportation
permission
workspace
```

If the user lacks money, the live problem becomes:

```text
How do I get money for the repair?
```

If the user lacks tools, the live problem becomes:

```text
Where can I borrow, rent, substitute, or access tools?
```

The root problem becomes a tree of smaller acquisition problems. A foreground LLM can generate this tree once. CASPER's proposed move is to keep the tree alive in the background and test new daily context against it.

## 2. The Core Mechanism

The mechanism has five stages.

```text
1. Problem capture
2. Requirement graph construction
3. Heartbeat context sampling
4. Associative bridge search
5. Candidate path surfacing
```

### 2.1 Problem Capture

The system stores two representations of the unresolved problem.

```text
plain problem:
  "I need to fix my vehicle."

CASCADE decode:
  object: vehicle
  desired transition: broken -> usable
  primary mechanisms: repair, restore, re-enable, replace, workaround
  missing requirements: unknown
  constraints: money, tools, knowledge, parts, time, access
```

The plain problem preserves user intent. The CASCADE decode strips the problem down to mechanics.

### 2.2 Requirement Graph Construction

CASCADE expands the problem into a graph of needed conditions.

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
  -> pay for unavailable parts/service
     -> price
     -> budget
     -> money
  -> if money absent
     -> earn money
     -> borrow money
     -> trade service
     -> reduce cost
     -> find substitute
```

Each requirement can become its own subproblem:

```text
knowledge -> where to learn?
tools -> where to get?
parts -> where to source?
service -> who can perform?
money -> how to obtain?
```

This graph gives the background agent many targets. It does not need to solve the whole vehicle problem at once. It can look for progress on any unsatisfied branch.

### 2.3 Heartbeat Context Sampling

The background agent runs periodically. The interval can be hourly, daily, or event-triggered.

At each heartbeat it checks fresh context:

```text
latest conversation with user
notes and logs
clipboard fragments
project files
messages
calendar entries
local documents
news
recent browsing or research traces
```

It extracts:

```text
salient nouns
verbs
events
places
people
services
objects
prices
skills
tools
offers
constraints
opportunities
```

The important design choice is that the agent does not only look for words that match the original problem. It looks for words that could satisfy a requirement.

### 2.4 Associative Bridge Search

Each extracted word or situation is expanded through nearby associations.

```text
seed word
  -> close phrase
  -> related situation
  -> underlying mechanism
  -> requirement match
```

This follows the practical "closest related words" behavior of an LLM: adjacent phrases, common contexts, nearby meanings, and ordinary sentence completions. The system uses that tendency deliberately, but constrains it with the requirement graph.

Example:

```text
daily signal:
  "The barbecue at my dad's house was good."

lexical expansion:
  barbecue
  barbecue party
  grilled food
  prepared food
  people buying food
  barbecue service
  selling plates

mechanism extraction:
  prepare desirable food -> exchange for money

requirement match:
  money branch is unsatisfied

candidate path:
  barbecue skill/event could become a small money-generation path
```

The bridge is not topical. Barbecue is not a vehicle-repair concept. The bridge is functional:

```text
barbecue -> service -> money -> repair requirement
```

This is the core of the mechanism.

### 2.5 Candidate Path Surfacing

The agent returns compact candidate paths, not free-form inspiration.

```text
source signal:
  "BBQ at dad's house was good."

association chain:
  BBQ -> prepared food -> informal food service -> money

matched requirement:
  vehicle repair requires money

candidate action:
  explore whether a small barbecue plate sale, catering favor,
  or related food-prep gig could fund part of the repair

confidence:
  low-to-medium; requires feasibility check
```

The chain must be visible. Without the chain, the user cannot distinguish useful lateral thought from noise.

## 3. Why This Is Not Ordinary Task Decomposition

Task decomposition breaks a problem into substeps. That part is not new.

Requirement-guided associative incubation adds a second loop:

```text
decomposed requirement graph
  + fresh unrelated context
  + lexical/semantic expansion
  + mechanism matching
  -> opportunistic solution path
```

A normal planner says:

```text
You need money. Get a job, sell something, borrow, or save.
```

The proposed background agent says:

```text
You mentioned BBQ yesterday.
BBQ can become a small food service.
Food service can generate money.
Money satisfies the vehicle-repair branch.
Do you want to evaluate that path?
```

The difference is opportunistic grounding. The suggestion comes from the user's actual context rather than a generic list.

## 4. Why This Is Not Random Association

Random association starts with a random word and asks the model to be creative.

This mechanism starts with an unsatisfied requirement. A daily word is only useful if it can bridge into that requirement.

```text
random word:
  barbecue

unchecked association:
  barbecue -> summer -> beach -> vacation

requirement-guided association:
  barbecue -> prepared food -> paid service -> money -> vehicle repair
```

The graph acts as a filter. It asks:

```text
Which branch does this association help?
What requirement does it satisfy?
What action does it imply?
What source supports it?
What uncertainty remains?
```

This prevents the system from treating any clever connection as useful.

## 5. Formal Model

Let the unresolved problem be:

```text
P
```

CASCADE converts `P` into a requirement graph:

```text
G = (R, E)
```

Where:

```text
R = requirement nodes
E = dependency edges
```

Each requirement node has:

```text
id
description
status: satisfied | unsatisfied | blocked | unknown
type: knowledge | tool | part | service | money | access | skill | time | permission | other
constraints
candidate_paths
```

At heartbeat `t`, the agent samples context:

```text
C_t = fresh context at time t
```

It extracts seeds:

```text
S_t = terms, events, people, places, objects, mechanisms from C_t
```

Each seed is expanded:

```text
A(s) = lexical and semantic neighbors of seed s
```

The agent then searches for a bridge:

```text
B = s -> a_1 -> a_2 -> ... -> mechanism -> requirement r
```

A bridge is useful only if it improves a requirement node:

```text
score(B, r) = relevance + mechanism_fit + actionability + novelty + traceability - risk
```

The agent surfaces high-scoring bridges as candidate paths.

## 6. Agent Loop

The heartbeat agent can be written as:

```text
for each heartbeat:
  load active unresolved problems
  for each problem:
    load requirement graph
    read fresh context since last heartbeat
    extract candidate seeds
    expand each seed through lexical neighbors
    infer mechanism for each expansion chain
    compare mechanism against unsatisfied requirements
    score candidate bridges
    store all candidates
    surface only candidates above threshold
```

The agent should work on many branches in parallel:

```text
money branch
tools branch
parts branch
knowledge branch
service branch
access branch
```

This is important because a problem may become solvable through any branch. The agent should not overcommit to the obvious path.

## 7. Example: Vehicle Repair

### 7.1 Root Problem

```text
I need to fix my vehicle.
```

### 7.2 Mechanism Decode

```text
desired transition:
  unusable vehicle -> usable vehicle

possible solution mechanisms:
  repair
  restore
  replace
  re-enable
  bypass
  outsource
```

### 7.3 Requirement Graph

```text
fix vehicle
  -> diagnose
     -> knowledge
     -> inspection
  -> repair
     -> tools
     -> parts
     -> workspace
     -> skill
  -> outsource
     -> mechanic/service
     -> price
     -> transportation
  -> fund
     -> money
     -> budget
     -> earning path
     -> cost reduction
```

### 7.4 Heartbeat Signal

```text
User said:
  "BBQ at dad's house was really good this week."
```

### 7.5 Lateral Expansion

```text
BBQ
  -> barbecue party
  -> grilled food
  -> prepared meals
  -> food people pay for
  -> local food sale
  -> quick cash
```

### 7.6 Mechanism Match

```text
bridge mechanism:
  prepare valued food -> sell/trade -> money

matched requirement:
  repair requires money
```

### 7.7 Candidate Output

```text
Candidate:
  The BBQ context may imply a small money-generation path.

Why:
  The vehicle repair graph has an unsatisfied money branch.
  BBQ maps to a sellable prepared-food service.

Action:
  Estimate whether a one-day BBQ plate sale, catering favor,
  or family-network food order could cover a specific repair cost.

Next check:
  repair estimate, available kitchen/grill, legal/local constraints,
  ingredient cost, expected buyers.
```

The agent has not solved the repair. It has found a possible branch to investigate.

## 8. Output Schema

Each surfaced candidate should preserve the path.

```json
{
  "problem_id": "problem_vehicle_repair_001",
  "heartbeat": "2026-06-26T00:00:00-04:00",
  "source_signal": {
    "type": "conversation",
    "excerpt": "BBQ at dad's house was really good this week."
  },
  "seed": "BBQ",
  "association_chain": [
    "BBQ",
    "prepared food",
    "informal food service",
    "people pay for food",
    "money"
  ],
  "inferred_mechanism": "convert existing food-prep context into a small paid service",
  "matched_requirement": {
    "id": "req_money",
    "type": "money",
    "description": "fund vehicle repair"
  },
  "candidate_path": "Evaluate whether a small BBQ sale or food-prep job could fund part of the repair.",
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

## 9. Relationship To Existing Work

The pieces of this mechanism are related to prior research.

### 9.1 Task Decomposition And Planning

LLM agents already decompose tasks into subgoals, plans, and tool calls. Requirement-guided incubation uses decomposition, but the graph is not only a plan. It becomes a persistent filter over future context.

### 9.2 Associative Thinking And Random Words

Creativity systems often inject unrelated words or ask models to form associations. This mechanism does use lexical association, but it constrains association with unsatisfied requirements. A word is useful only if it can help a branch of the graph.

### 9.3 Literature-Based Discovery

Literature-based discovery uses indirect A-B-C links to reveal hidden relationships. Requirement-guided incubation uses a similar bridge pattern, but the target is a user's live problem rather than a fixed scientific corpus.

### 9.4 Agent Memory Systems

Memory agents store experiences, retrieve relevant events, and synthesize reflections. This proposal treats new memories and daily signals as possible resources for live unsolved requirements.

### 9.5 Cognitive Incubation

Human problem solving often benefits from incubation: after a failed direct attempt, later experiences can trigger a new angle. This paper proposes an engineered analogue: the agent periodically re-tests fresh signal against the problem's requirement graph.

## 10. Novelty Claim

The broad ingredients are not new:

- task decomposition;
- semantic association;
- random-word creativity;
- agent memory;
- analogy;
- literature-based discovery;
- serendipitous recommendation.

The narrower claim is:

> A failed or unresolved user problem can be converted into a persistent requirement graph, and a heartbeat agent can use that graph to filter daily context for lateral associations that satisfy blocked requirements.

The contribution is the combination:

```text
unsolved problem
  -> mechanism decode
  -> requirement graph
  -> parallel unsatisfied branches
  -> heartbeat context sampling
  -> closest-association expansion
  -> mechanism bridge test
  -> candidate path with inspectable chain
```

## 11. Evaluation Plan

The mechanism can be tested without claiming success upfront.

### 11.1 Benchmark Items

Create a set of unresolved practical problems:

```text
fix vehicle
find collaborator
reduce project cost
obtain tool access
learn unfamiliar skill
recover blocked workflow
find local help
generate small amount of money
```

Each item should include:

```text
root problem
known constraints
ground-truth or human-rated solution paths
daily-context stream containing relevant and irrelevant signals
```

### 11.2 Conditions

Compare:

```text
A. Direct prompt only
B. Direct prompt plus task decomposition
C. Direct prompt plus random-word association
D. Requirement graph only
E. Requirement graph plus daily-context seeds
F. Full heartbeat agent with associative bridge scoring
```

### 11.3 Metrics

Human judges blind-score:

```text
usefulness
novelty
requirement fit
actionability
traceability
false-bridge rate
cost or risk awareness
```

The decisive comparison is:

```text
F vs B:
  does heartbeat associative incubation beat ordinary decomposition?

F vs C:
  does requirement filtering beat random association?

E vs D:
  does daily context add useful opportunity signals?
```

## 12. Implementation Sketch

Minimal storage:

```text
problem_store/
  problem.json
  cascade_decode.json
  requirement_graph.json

heartbeat_store/
  context_samples.jsonl
  extracted_seeds.jsonl
  bridge_candidates.jsonl
  surfaced_candidates.jsonl

feedback_store/
  accepted_paths.jsonl
  rejected_paths.jsonl
  decayed_paths.jsonl
```

Minimal modules:

```text
problem_intake.py
  records unresolved problem and plain-language goal

cascade_requirements.py
  builds requirement graph and blocked branches

heartbeat_sampler.py
  reads fresh context since last heartbeat

seed_extractor.py
  extracts words, places, people, objects, services, prices, and events

association_expander.py
  expands seeds into close lexical and semantic neighbors

mechanism_mapper.py
  converts association chains into mechanism descriptions

requirement_matcher.py
  tests mechanisms against unsatisfied branches

bridge_scorer.py
  scores usefulness, novelty, traceability, and risk

candidate_reporter.py
  surfaces compact chains for user review
```

## 13. Safety And Failure Modes

This system can produce bad suggestions if every association is treated as meaningful. The requirement graph reduces noise, but it does not eliminate it.

Major failure modes:

- false bridges that sound clever but do not help;
- over-personal mining of private context;
- unsafe or illegal money-generation suggestions;
- overconfident inference from weak signals;
- too many low-value candidate paths;
- confusing "possible" with "worth doing."

Controls:

- keep source chains visible;
- require user review before action;
- score risk and feasibility;
- suppress low-actionability bridges;
- allow user to reject a branch permanently;
- decay unvalidated suggestions.

## 14. Conclusion

Requirement-guided associative incubation turns an unsolved problem into a standing background search.

The system does not wait for the user to restate the problem. It decomposes the problem into requirements, runs parallel searches over those requirements, and periodically tests fresh context for useful lateral bridges. A random daily word becomes relevant only when it maps to an unsatisfied branch.

The important example is:

```text
BBQ -> prepared food -> paid service -> money -> vehicle repair
```

That chain captures the mechanism. The agent is not asking whether BBQ is about vehicles. It is asking whether BBQ contains a mechanism that can satisfy one of the vehicle problem's missing requirements.

That is the paper's core claim: useful novelty can be produced by combining requirement graphs with opportunistic associative bridges over daily context.

---

## Appendix A - One-Sentence Claim

A background LLM agent can improve unresolved problem solving by converting the problem into a requirement graph, then using periodic context sampling and closest-association expansion to find daily signals whose mechanisms satisfy blocked requirements.

## Appendix B - Source Anchors

- Mehrotra, Parab, and Gulwani, ["Enhancing Creativity in Large Language Models through Associative Thinking Strategies"](https://arxiv.org/abs/2405.06715), arXiv:2405.06715.
- Lee et al., ["Spacer: Towards Engineered Scientific Inspiration"](https://arxiv.org/abs/2508.17661), arXiv:2508.17661.
- Park et al., ["Generative Agents: Interactive Simulacra of Human Behavior"](https://arxiv.org/abs/2304.03442), arXiv:2304.03442.
- Gutierrez et al., ["HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models"](https://arxiv.org/abs/2405.14831), arXiv:2405.14831.
- Rasmussen et al., ["Zep: A Temporal Knowledge Graph Architecture for Agent Memory"](https://arxiv.org/abs/2501.13956), arXiv:2501.13956.
- Alkan et al., ["A Survey on Hypothesis Generation for Scientific Discovery in the Era of Large Language Models"](https://arxiv.org/abs/2504.05496), arXiv:2504.05496.
- Smalheiser, ["Rediscovering Don Swanson: the Past, Present and Future of Literature-based Discovery"](https://pmc.ncbi.nlm.nih.gov/articles/PMC5771422/), Journal of Data and Information Science, 2017.
- Sio and Ormerod, ["Does incubation enhance problem solving? A meta-analytic review"](https://pubmed.ncbi.nlm.nih.gov/19210055/), Psychological Bulletin, 2009.
- Frontiers review, ["Incubation and Intuition in Creative Problem Solving"](https://pmc.ncbi.nlm.nih.gov/articles/PMC4956660/), Frontiers in Psychology, 2016.
