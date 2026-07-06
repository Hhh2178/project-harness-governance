---
name: project-harness-governance
description: Use when starting or restructuring a medium/large software project that needs durable agent rules, documentation architecture, harness verification, visual standards, component registries, project overview files, logs, plans, indexes, and ongoing governance boundaries.
---

# Project Harness Governance

## Overview

Build the project operating layer before feature work: agent constitution, project overview, docs router, system knowledge, logs or ledger, visual standards, reusable component registries, interface docs, and verification scripts. The goal is a durable "AI-executable harness" that lets future agents enter, understand, change, verify, and audit the project without guessing.

This skill stops at harness/governance scaffolding. Use other skills for feature implementation, bug diagnosis, UI implementation, code review, QA, release, and deployment.

## Scope Boundary

Use this skill to create or repair the project harness:

- Root entries: `AGENTS.md`, `README.md`, memory/log/ops compatibility entries.
- Documentation map: `docs/INDEX.md`, `docs/governance/`, `docs/systems/`, `docs/logbooks/`, `docs/superpowers/`.
- Harness map: verification scripts, release gates, workspace checks, contract checks, optional ledger/CLI evidence layer.
- Frontend/admin design standards: tokens, visual language, component registries, verification checklists.
- Technical stack and interface docs: system interface templates, env/runtime maps, permissions, data flow.

Do not use this skill to implement business features, refactor large code paths, ship releases, or run product QA. Hand those to the appropriate execution skills after the harness exists.

## Workflow

1. Inspect the current project state before editing.
   - Run `git status --short`.
   - Read existing root entries, docs indexes, package scripts, and recent logs.
   - Identify whether this is a new project, dirty existing project, or rescue/restructure.
   - If the worktree is dirty, classify each change as user work, harness work, generated artifact, or unknown before touching files.

2. Choose the governance mode.
   - Use lightweight doc-log mode by default: `docs/logbooks/` is the evidence trail, and package scripts provide verification gates.
   - Use ledger mode only for long-running, multi-agent, high-audit, or high-risk projects where task status, decisions, reviews, costs, screenshots, and verification evidence need a queryable local database.
   - Do not introduce a ledger/CLI layer into an existing project without checking for conflicts with current issue tracking, release logs, and documentation rules.

3. Create the authority model.
   - Make `AGENTS.md` the agent constitution: rules, boundaries, reading order, verification duties, update duties, and forbidden actions.
   - Make `README.md` the human/project overview: what the project is, how to run it, current state, main links, and contribution path.
   - Make `docs/INDEX.md` the docs router: canonical locations, update rules, and where to record decisions.
   - Keep `MEMORY.md`, `DEVLOG.md`, and `ops/` as compatibility entries when they exist, but point them to canonical docs instead of duplicating facts.
   - If ledger mode is selected, make the ledger the canonical source for task status, decisions, evidence, reviews, costs, and visual changes; docs remain the canonical source for durable rules and system contracts.

4. Create the docs structure.
   - Governance: rules, archive policy, worktree/release boundaries.
   - Systems: API, frontend/canvas, admin, worker, providers, auth/users, storage/data, observability/ops, harness.
   - Logbooks: daily, releases, validations, incidents.
   - Plans/specs: design and implementation planning documents.
   - Every created document must have an owner, purpose, required sections, update trigger, and anti-duplication rule.

5. Define harness checks.
   - Add contract scripts for entry consistency, docs indexes, visual docs, component registries, package exports, release state, runtime artifacts.
   - Wire aggregate commands such as `harness:verify:project`, `harness:verify:workspace`, and `harness:verify:release`.
   - If ledger mode is selected, include a local CLI such as `bin/harness verify` and evidence output such as `ledger/evidence/`.
   - If the repo has hooks, connect non-invasive governance checks to pre-commit.

6. Define visual and component governance.
   - Frontend/canvas: design tokens, node composition patterns, visual component registry, functional component registry.
   - Admin/backend UI: tokens, layout density, table/form/drawer rules, component library policy, component registries.
   - Do not install component libraries or rewrite UI unless the user explicitly asks for implementation.

7. Define the maintenance loop.
   - Start of task: read `AGENTS.md`, `README.md`, `docs/INDEX.md`, current-state docs, and latest logbook.
   - In ledger mode: inspect the ledger summary and create/update the active task before meaningful edits.
   - During task: update plans/specs before risky implementation, keep source-of-truth boundaries intact, and avoid undocumented side paths.
   - End of task: run harness verification, update logs or ledger evidence, update affected indexes, record unresolved risks, and leave the worktree state explicit.

8. Leave audit evidence.
   - Record what changed, why, verification, risks, and next steps in daily logbooks or ledger evidence.
   - Commit in small boundaries: docs architecture, visual standards, contracts, log evidence.

## Required Outputs

For a fresh or major restructure, aim to produce:

- `AGENTS.md`
- `README.md`
- `docs/INDEX.md`
- `docs/governance/root-entry-responsibility-matrix.md`
- `docs/systems/README.md`
- `docs/systems/harness/README.md`
- `docs/systems/interface-documentation-template.md`
- `docs/systems/<frontend>/frontend-design/`
- `docs/systems/<admin>/frontend-design/`
- `docs/logbooks/daily/`
- `docs/logbooks/releases/`
- `docs/superpowers/specs/`
- `docs/superpowers/plans/`
- `scripts/verify-*-contract.*`
- root package/script entries that run the checks
- Optional ledger mode: `bin/harness`, `ledger/schema.sql`, `ledger/ledger.py`, `ledger/evidence/`, and ledger-aware verification.

For a small project, compress the same model into fewer files, but keep the authority boundaries clear.

## File Content Contract

Every harness file must answer these questions:

- What is this file responsible for?
- Who or what must read it first?
- What facts are canonical here?
- What facts must be linked elsewhere instead of duplicated?
- When must this file be updated?
- Which verification checks protect it?

Minimum required contents:

- `AGENTS.md`: constitution, project root, reading order, safety rules, worktree rules, secret handling, edit rules, verification commands, logging duties, release boundaries, and "stop and ask" conditions.
- `README.md`: product purpose, architecture summary, current branch/environment state, local setup, main commands, docs map, deployment summary, and active work status.
- `docs/INDEX.md`: docs taxonomy, canonical source table, update triggers, archive policy pointer, and fast path for new agents.
- `docs/governance/*`: durable rules for documentation, engineering guardrails, worktree boundaries, release/version policy, and history/archive policy.
- `docs/systems/*`: one system per folder with purpose, ownership, interfaces, data flow, permissions, runtime/env, failure modes, tests, and change log.
- `docs/systems/*/frontend-design/*`: concrete design tokens, visual components, functional components, composition patterns, and verification checklist.
- `docs/logbooks/*`: append-only evidence of date, intent, changed files, verification, decisions, risks, and next action.
- Optional `ledger/*`: queryable task, decision, evidence, review, cost, and visual-change records for projects that need stronger auditability than markdown logs.
- `docs/superpowers/specs/*`: design intent, requirements, constraints, data/API contracts, acceptance criteria, and non-goals.
- `docs/superpowers/plans/*`: executable phases, touched files, verification per phase, rollback path, and completion checklist.
- `scripts/verify-*`: deterministic checks for stable anchors; they should fail loudly and explain the remediation.

## Decision Rules

- Root files summarize and link; they do not hold long histories.
- One fact has one canonical source.
- Governance docs explain rules; system docs explain how systems work; logbooks prove what happened.
- Visual standards must include concrete values, not only adjectives.
- Component registries must separate visual components from functional modules.
- Verification scripts should check stable anchors, not brittle prose.
- Never use docs as a substitute for automated checks when a check is practical.
- Do not create decorative docs. Every file must be either an authority, router, template, log, or verification target.
- Do not let harness docs drift from runtime reality. If a claim can change by deployment, version, command, or branch, give it an update trigger and a verification path.
- Do not use both markdown logs and ledger as equal sources for task status. If ledger mode is active, markdown logs are supplemental narrative records.
- Do not force ledger mode into small projects or already-governed projects unless the added operational cost is justified.

## References

Read `references/harness-blueprint.md` when creating or repairing harness files. It contains the concrete file tree, required file templates, AGENTS constitution template, maintenance loop, script ideas, visual token categories, component registry schemas, and phased rollout plan.
