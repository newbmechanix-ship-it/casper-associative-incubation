# Harness Scaffold

This directory is reserved for a future implementation.

The intended harness should provide:

```text
init
assign problem
build requirement graph
expand requirement branches
discover compartments
manual incubation run
optional scheduled heartbeat
candidate report writing
feedback capture
promotion and decay
```

Recommended local runtime directory:

```text
.associative-incubation/
```

Do not commit runtime data from a user's local installation.

## Minimal Future Module Plan

```text
problem_intake.py
  creates active problem records

requirement_graph.py
  decomposes problems into requirements and blocked branches

branch_expander.py
  expands blocked requirements into memory, public-channel, program, substitution, and lateral branches

compartment_discovery.py
  discovers local knowledge compartments with user consent

context_sampler.py
  samples changed context from enabled compartments

seed_extractor.py
  extracts words, objects, events, services, prices, skills, and mechanisms

association_expander.py
  expands seeds into close lexical and semantic neighbors

mechanism_matcher.py
  maps chains to unsatisfied requirements

memory_probe.py
  searches enabled compartments for entities, affiliations, assets, skills, and relationships that may satisfy requirements

bridge_scorer.py
  scores relevance, novelty, actionability, traceability, and risk

candidate_writer.py
  writes inspectable candidate reports

feedback.py
  captures user accept/reject/decay signals
```
