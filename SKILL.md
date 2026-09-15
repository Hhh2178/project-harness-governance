---
name: project-harness-governance
description: Use when starting, restructuring, or maintaining a project repository that needs durable Codex guidance, clear document ownership, requirements and acceptance records, current-state tracking, verification contracts, and an auditable work log.
---

# Project Harness Governance

## Purpose

Create and maintain a repository-level Harness that lets Codex work on the same project across tasks and sessions without guessing. The Harness is the project's durable governance layer: rules, project knowledge, verification, and evidence. It is not an Agent runtime, orchestration platform, context engine, product feature, or replacement for tests and code review.

Use this skill to establish or repair the Harness before substantial feature work, and to keep its records aligned as the project evolves.

## Scope Boundary

This skill may create or repair `AGENTS.md`, `README.md`, `docs/` requirements, current state, systems, decisions, plans, logs, validation evidence, deterministic Harness checks, and optional lightweight or Ledger evidence tracking. It may document optional local tools such as CodeGraph and RTK.

Do not use it to implement product features, build an Agent, introduce a context database, install global hooks, deploy services, or run product QA.

## Operating Model

Keep four concerns separate:

1. **Constitution** - what Codex must obey (`AGENTS.md`).
2. **Project knowledge** - what the project is, should become, and currently is.
3. **Execution contracts** - what must be checked before work is accepted.
4. **Evidence** - what changed, why, and what verification proved.

One fact has one canonical source. Root files summarize and route; they do not become diaries or encyclopedias. Prefer the smallest structure that gives the project reliable continuity.

## Workflow

1. **Inspect before editing.** Run `git status --short`; locate the project root, existing instruction files, README, docs, package manifests, scripts, CI, recent logs, and user changes. Classify dirty changes before touching them.
2. **Choose the smallest governance mode.** Use lightweight doc-log mode by default. Choose Ledger mode only when queryable task/evidence history is justified by project scale, audit risk, or an explicit request. Record the decision.
3. **Establish authority.** Create or repair `AGENTS.md`, `README.md`, `docs/INDEX.md`, and a short `docs/current-state.md`. Add requirements, systems, decisions, plans, logs, and validation folders only when useful.
4. **Write project-specific rules.** Record real commands, boundaries, ownership, acceptance criteria, and risks. Do not copy placeholders or invent commands.
5. **Add checks.** Prefer small deterministic scripts for stable anchors, document routing, command consistency, secret ignores, and relevant project verification. Keep all checks runnable without optional tools.
6. **Detect optional tools.** If CodeGraph or RTK is present, document only project-relevant usage, status, and fallback. Never make them product dependencies or change global configuration without explicit approval.
7. **Maintain continuously.** At task start read the root entries, current state, and only documents routed by the task. At task end, perform the documentation impact check below, run relevant verification, and append evidence.

## Required Reading Contract

Every task starts with this bounded read:

1. `AGENTS.md`
2. `README.md`
3. `docs/INDEX.md`
4. `docs/current-state.md`
5. `git status --short`

Then follow `docs/INDEX.md` only to requirement, plan, system, decision, or log documents relevant to the task. Do not load the entire documentation tree by default.

## Documentation Authority Model

| Fact | Canonical source |
| --- | --- |
| Agent rules and reading order | `AGENTS.md` |
| Stable project purpose and setup | `README.md` |
| Long-term goals and non-goals | `docs/requirements/product-goals.md` |
| Phase scope and constraints | `docs/requirements/scope.md` |
| Acceptance conditions | `docs/requirements/acceptance-criteria.md` |
| Current phase, active work, risks, next step | `docs/current-state.md` |
| How a system works | `docs/systems/<system>/` |
| Why a durable choice was made | `docs/decisions/` |
| How approved work will be performed | `docs/plans/` or `docs/superpowers/plans/` |
| What happened | `docs/logbooks/` |
| Verification evidence | `docs/validations/` |

Do not maintain two equal sources for task status. In Ledger mode, the ledger owns task status and evidence; Markdown logs are supplemental narrative.

## Documentation Impact And Confirmation

After every meaningful change, answer:

1. What behavior, interface, command, permission, runtime assumption, or project structure changed?
2. Which canonical document owns that fact?
3. Does the document still match the repository?
4. Is the result `no update needed`, `routine record`, `proposed authority update`, or `conflict requiring user decision`?

Automatically append routine logs, validation evidence, confirmed progress, and known risks. Before changing `AGENTS.md`, project purpose, scope, acceptance criteria, architecture, security or deployment policy, validation gates, or an approved decision, show the discrepancy and proposed files to the user and wait for confirmation. Never silently resolve a code/documentation conflict. Record the decision after confirmation.

## Tool Protocols

### CodeGraph

CodeGraph is optional navigation support for unfamiliar repositories, cross-file impact analysis, and structural refactors. Use it only when the task warrants it; confirm important findings against current source and tests. If unavailable or stale, use `rg`, language tooling, and direct inspection. It is never required for setup, build, test, release, or Harness verification.

### RTK

RTK is optional shell-output compression. Verification must work with native commands. Use native commands when compact output is incomplete or diagnosis needs the raw stream. Do not change global RTK hooks as part of project work without explicit user approval.

## Completion Contract

Before declaring Harness work complete:

- Root entries and document ownership are coherent.
- Requirements, current state, plans, and evidence are not conflated.
- Relevant checks run and results are recorded.
- Documentation impact was classified.
- Required user confirmations were obtained.
- Unresolved risks and the next action are explicit.
- `git status --short` is reported.

Read `references/harness-blueprint.md` first. It is an index: follow only the routed reference needed for the task (`lifecycle-and-modes.md`, `root-and-authority-contracts.md`, `systems-and-interface-contracts.md`, `frontend-and-admin-standards.md`, `evidence-and-verification.md`, or `ledger-and-optional-tools.md`). Do not load every reference by default.
