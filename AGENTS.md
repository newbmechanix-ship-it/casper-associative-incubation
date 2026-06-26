# Agent Instructions

This repository describes an experimental Associative Incubation Harness.

If asked to install it:

1. Install into a local workspace directory named `.associative-incubation/`.
2. Do not create automatic background LLM calls by default.
3. Require explicit user assignment before creating an active problem.
4. Discover local knowledge compartments dynamically; do not assume fixed modules.
5. Ask before enabling sensitive compartments.
6. Decompose assigned problems into requirement graphs.
7. Expand blocked requirements into budgeted branch families.
8. Probe enabled memory compartments for entities, affiliations, assets, skills, and relationships that may satisfy requirements.
9. Search fresh context for mechanism bridges that satisfy blocked requirements.
10. Surface candidate paths with source chains, risk, uncertainty, and required user review.
11. Never take external actions without explicit user approval.
12. Keep runtime data local and out of public commits.

Primary docs:

- `docs/INSTALL_FOR_CODEX_OR_CLAUDE_CODE.md`
- `docs/AGENTIC_HARNESS_SPEC.md`
- `docs/TOKEN_AND_SAFETY_MODEL.md`
