# CASPER Associative Incubation

![CASPER Associative Incubation banner](assets/banner.png)

A research proposal and experimental harness design for giving a coding agent a voluntary background problem-incubation capability.

The system is not a fixed personal daemon layout. It is a generic mechanism that can be installed into a user's own agent workspace, discover whatever knowledge compartments already exist there, and run only when the user explicitly assigns an unresolved problem.

## Core Idea

```text
user assigns unresolved problem
  -> agent builds a requirement graph
  -> agent expands requirements into many possible solution branches
  -> agent discovers local knowledge compartments
  -> heartbeat pass samples fresh context and memory
  -> lateral association, memory probes, and public-channel probes find bridges
  -> candidate paths are surfaced for review
  -> user accepts, rejects, promotes, or decays them
```

Example:

```text
Problem:
  Need money to fix a vehicle.

Daily signal:
  "The BBQ at dad's house was good."

Bridge:
  BBQ -> prepared food -> paid service -> money -> vehicle repair
```

The bridge is not topical. BBQ is not about vehicle repair. The bridge is functional: a daily-context signal contains a mechanism that may satisfy an unsolved requirement.

Second example:

```text
Problem:
  Need a way to reach a target institution.

Requirement:
  access / credibility / warm introduction / official channel

Memory probe:
  known people -> affiliations -> possible institutional connection

Bridge:
  known person -> public affiliation -> advice/referral/channel -> target institution
```

This shows the other search direction. The system does not only wait for daily context to produce a clue. It can also start from an unsatisfied requirement and probe memory for entities, relationships, affiliations, public programs, official channels, and second-degree paths that might satisfy it.

## Repository Layout

```text
papers/
  Agentic_Associative_Incubation_Harness_paper.md
  Associative_Retrieval_research_note.md
  CASPER_Longitudinal_Keyword_Pathways_paper.md
  CASPER_Requirement_Guided_Associative_Incubation_paper.md

docs/
  AGENTIC_HARNESS_SPEC.md
  INSTALL_FOR_CODEX_OR_CLAUDE_CODE.md
  TOKEN_AND_SAFETY_MODEL.md

harness/
  README.md

examples/
  assigned_problem.example.json
  branch_expansion.example.json
  bridge_candidate.example.json
  access_bridge_candidate.example.json
  compartments.example.json
```

## Important Safety Rule

This is experimental. It should not create an always-on LLM spending loop by default.

The background agent should run only when:

```text
1. the user explicitly assigns a problem;
2. the user sets a budget or cadence;
3. the agent records each run;
4. the user can pause or delete the background task.
```

## Installation Target

This is meant to be installed by a coding agent such as Codex or Claude Code into the user's own project or agent workspace.

Start with:

[papers/Agentic_Associative_Incubation_Harness_paper.md](papers/Agentic_Associative_Incubation_Harness_paper.md)

Then read:

[docs/INSTALL_FOR_CODEX_OR_CLAUDE_CODE.md](docs/INSTALL_FOR_CODEX_OR_CLAUDE_CODE.md)

Then read:

[docs/AGENTIC_HARNESS_SPEC.md](docs/AGENTIC_HARNESS_SPEC.md)

## Status

Working paper and harness specification. The repository should be treated as a proposal and experimental scaffold until benchmark results exist.
