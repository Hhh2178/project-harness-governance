# Harness Blueprint Reference

This reference defines what a project harness is, how to start it, what each file must contain, and how to keep it alive during long-running development.

## 1. Harness Purpose

A project harness is the operating system around the codebase. It gives agents and humans a stable way to:

- Find the project root, active branch, environments, and current state.
- Understand the rules before modifying files.
- Locate canonical docs instead of guessing.
- Keep frontend/admin visual design consistent.
- Reuse visual and functional components.
- Verify that documentation, scripts, package exports, and release state still agree.
- Leave audit evidence after every meaningful change.

The harness is not product implementation and does not build an Agent runtime,
orchestration platform, context engine, or project-specific tool platform. It
is a repository-level governance layer that helps Codex maintain the project
across tasks and sessions.

Optimize for attention and token economy: keep the root constitution short,
route to documents instead of repeating them, read only task-relevant material,
and prefer deterministic checks over long instructions.

## 2. Start Procedure

Use this sequence when starting or restructuring a medium/large project:

1. Run `git status --short` and classify existing changes.
2. Read existing `AGENTS.md`, `README.md`, `MEMORY.md`, `DEVLOG.md`, `docs/`, `ops/`, package scripts, and recent commits.
3. Identify canonical facts: project name, active root, branch/worktree, environments, tech stack, main commands, deploy path, secrets policy, and current roadmap.
4. Choose lightweight doc-log mode or ledger mode.
5. Decide whether to preserve, redirect, or replace old docs.
6. Create or repair root entries first.
7. Create docs router and governance docs.
8. Create system docs and interface template.
9. Create frontend/admin design standards and component registries.
10. Add verification scripts for stable anchors.
11. Update logbooks or ledger with changed files, purpose, verification, risk, and next step.
12. Run verification and leave `git status --short` explicit.

Do not begin feature work until root entry and docs routing are coherent.

## 2.1 Governance Mode Selection

Choose one primary evidence model before creating files.

| Mode | Use When | Canonical Task Status | Evidence | Cost |
| --- | --- | --- | --- | --- |
| Lightweight doc-log mode | Small or medium projects, existing repos, low ceremony, simple audit needs | `docs/logbooks/` plus plans/specs | Markdown logs and verification output | Low |
| Ledger mode | Long-running projects, multi-agent work, high-risk deploys, many decisions/reviews/screenshots/cost records | `ledger/` database | `ledger/evidence/` plus CLI records | Medium |

Default to lightweight mode unless the project clearly needs queryable task/evidence records.

Use ledger mode when at least two are true:

- Multiple agents or tools will work on the same project over time.
- The project has frequent releases, gray/prod environments, or production risk.
- Task status regularly drifts between chat, README, logs, and commits.
- Reviews, screenshots, validation reports, or cost records need durable search.
- The user explicitly wants a local governance CLI or database.

In ledger mode:

- `ledger/` owns task status, decisions, evidence, reviews, costs, and visual changes.
- `docs/logbooks/` becomes supplemental narrative history, not task truth.
- `AGENTS.md` must require reading ledger summary before meaningful work.
- Verification should write evidence into `ledger/evidence/` when practical.
- `ledger/ledger.db` or equivalent local generated state must be ignored by git.

Do not enable ledger mode by copying a whole template blindly. Adapt it to the existing project and record the decision.

## 3. Starter File Tree

```text
AGENTS.md
README.md
MEMORY.md
DEVLOG.md
ops/
  README.md
  current/
docs/
  INDEX.md
  governance/
    README.md
    root-entry-responsibility-matrix.md
    documentation-governance-standard.md
    engineering-guardrails.md
    worktree-and-branch-policy.md
    archive-policy.md
    secrets-and-access-policy.md
  requirements/
    README.md
    product-goals.md
    scope.md
    acceptance-criteria.md
  current-state.md
  decisions/
    README.md
  systems/
    README.md
    interface-documentation-template.md
    harness/
      README.md
      workspace-verify-release-map.md
    frontend/
      README.md
      frontend-design/
        design-tokens.md
        visual-component-registry.md
        functional-component-registry.md
        node-composition-patterns.md
        verification-checklist.md
    admin/
      README.md
      frontend-design/
        design-tokens.md
        component-library-policy.md
        visual-component-registry.md
        functional-component-registry.md
        verification-checklist.md
    api/
    worker/
    providers/
    auth-and-users/
    storage-and-data/
    observability-and-ops/
  logbooks/
    daily/
    releases/
    validations/
    incidents/
  superpowers/
    specs/
    plans/
scripts/
  verify-documentation-entry-contract.*
  verify-visual-design-docs-contract.*
  verify-component-registry-docs-contract.*
  verify-harness-doc-sync-contract.*
```

Compress this for small projects, but keep the same responsibilities.

## 3.1 Optional Ledger Mode File Tree

Add these only when ledger mode is selected:

```text
bin/
  harness
ledger/
  schema.sql
  ledger.py
  evidence/
    .gitkeep
skills/
  SKILL_REGISTRY.md
  setup-governance-harness.md
  maintain-docs-architecture.md
  run-harness-verification.md
  manage-ledger.md
scripts/
  verify_harness.py
  new_daily_log.py
.gitignore
```

Minimum ledger schema concepts:

- `tasks`: title, description, status, priority, created/updated timestamps.
- `decisions`: task id, decision type, content, rationale.
- `evidence`: task id, type, path or inline summary.
- `reviews`: task id, score, findings, blockers.
- `costs`: task id, token/time/money fields when relevant.
- `visual_changes`: token/component before/after values when relevant.

Minimum CLI capabilities:

- `setup`: initialize local generated state.
- `ledger init`: create local database.
- `ledger create-task`: start work.
- `ledger update-task`: update status.
- `ledger add-decision`: record durable choices.
- `ledger add-evidence`: attach verification output or screenshots.
- `ledger add-review`: attach review findings.
- `ledger summary`: show current state.
- `verify --write-evidence`: run harness checks and write evidence.

## 3.1 Minimality And Read Budget

Do not create every possible directory for a small project. Start with:

```text
AGENTS.md
README.md
docs/INDEX.md
docs/current-state.md
docs/requirements/
docs/logbooks/daily/
scripts/
```

Add systems, decisions, plans, validations, failures, visual registries, or
Ledger only when the project has a real need. Keep `AGENTS.md` roughly within
100-300 lines, keep `current-state.md` to a short snapshot, and make
`docs/INDEX.md` a routing table rather than a duplicate summary.

Every task reads the root entries and current state, then follows the index to
only the relevant requirement, plan, system, decision, or log. Full-tree
reading is reserved for Harness repair, release preparation, or explicit audit.

## 4. Root Entry Contracts

### `AGENTS.md` - Agent Constitution

Purpose: the first file an AI agent must obey before working.

Required sections:

- Project identity: project name, active root, legacy roots, and forbidden roots.
- Reading order: exact files to read before coding, deploying, or changing docs.
- Authority model: which files own current state, specs, plans, logs, release state, ops, and system docs.
- Safety rules: destructive command policy, secret handling, SSH/deploy restrictions, generated artifact handling.
- Worktree rules: active branch, dirty tree protocol, user-change protection, commit boundaries, no history rewrite unless explicitly requested.
- Editing rules: use existing patterns, avoid duplicate components, update indexes, preserve canonical sources.
- Verification duties: commands to run for docs, type-checks, tests, package exports, release checks, and local acceptance.
- Logging duties: when to update daily logs, validation logs, release logs, and incident logs.
- Stop-and-ask conditions: conflicting user changes, secret exposure, production risk, unclear branch, destructive operation, or schema migration risk.
- Maintenance block: who updates this file and what changes trigger updates.
- Documentation maintenance protocol: classify affected facts after meaningful
  changes and ask before changing authority documents.
- Optional tool policy: CodeGraph navigation and RTK output compression are
  non-essential, have documented fallbacks, and never become product
  dependencies.

If ledger mode is active, also include:

- Ledger root and generated database ignore rule.
- Required command for reading task status.
- Rule requiring task creation/update before meaningful work.
- Rule requiring evidence before marking tasks complete.
- Rule that markdown logs are supplemental, not task truth.

Must not contain:

- Long release history.
- Full feature specifications.
- Secrets, tokens, private keys, or copied server output.
- Stale branch/environment claims without update triggers.

Starter skeleton:

```markdown
# AGENTS.md - Project Agent Constitution

## Project Root
[active root, legacy roots, forbidden roots]

## First Reading Order
1. AGENTS.md
2. README.md
3. docs/INDEX.md
4. docs/memory/current-state.md or equivalent
5. latest daily log

## Authority Model
| Fact | Canonical Source | Update Trigger |
| --- | --- | --- |

## Safety Rules
[destructive commands, secrets, deployment, external systems]

## Worktree Rules
[dirty state, user changes, branch policy, commit policy]

## Edit And Verification Rules
[how to change files and what to run]

## Logging Rules
[what must be recorded and where]

## Stop And Ask
[conditions that require user confirmation]

## Documentation Maintenance Protocol
1. Identify changed behavior, interfaces, commands, permissions, runtime
   assumptions, and project structure.
2. Locate the canonical owner for each affected fact.
3. Classify each result as no update needed, routine record, proposed authority
   update, or conflict requiring user decision.
4. Append routine evidence automatically. Ask before changing this file,
   project purpose/scope, acceptance criteria, architecture, security or
   deployment policy, verification gates, or approved decisions.
5. Never silently resolve a code/documentation conflict.
```

### `README.md` - Human Project Overview

Purpose: a concise human-readable entrypoint.

Required sections:

- What this product is and who it serves.
- Current active branch/worktree and environment summary.
- Architecture snapshot: frontend, backend, workers, storage, providers, deployment shape.
- Local setup: prerequisites, install, env templates, run commands.
- Verification commands: type-check, test, build, harness verification.
- Deployment summary: gray/prod names, links, ports, and canonical runbooks.
- Documentation map: links to `docs/INDEX.md`, systems, plans, logs, ops.
- Current work status: only a short pointer, not a full log.
- Long-term product direction may be summarized here; detailed goals and
  acceptance conditions belong under `docs/requirements/`.

Must not contain:

- Duplicated deep system docs.
- Full deployment logs.

### Requirements And State

Keep these concerns separate:

- `docs/requirements/product-goals.md`: long-term goal, current phase goal,
  success signals, and non-goals.
- `docs/requirements/scope.md`: in-scope, out-of-scope, dependencies, and
  constraints for the current phase.
- `docs/requirements/acceptance-criteria.md`: functional, documentation, and
  verification conditions that define completion.
- `docs/current-state.md`: current phase, active work, recently completed work,
  known risks, next actions, and last verification. Keep it short and volatile.

Requirements are user-approved intent. Plans describe how to reach that intent.
Current state describes where the repository is now. Logs and validations prove
what happened. Do not use one file as a substitute for the others.
- Secrets or pasted env values.

### `MEMORY.md`

Purpose: cross-session memory and stable pointers.

Required sections:

- Current canonical project root.
- Current environment facts that are stable enough to remember.
- Links to canonical current-state, release, and ops docs.
- "Do not duplicate here" note for volatile facts.

### `DEVLOG.md`

Purpose: compatibility entry for older habits.

Required sections:

- Pointer to `docs/logbooks/daily/`.
- Latest log index link.
- Rule: new detailed records go to logbooks, not this file.

### `docs/INDEX.md`

Purpose: docs router and source-of-truth map.

Required sections:

- Fast path for new AI agents.
- Source-of-truth table.
- Docs taxonomy: governance, systems, logbooks, specs, plans, ops.
- Update triggers for each doc family.
- Archive policy pointer.
- Verification commands that protect docs.

If ledger mode is active, add:

- Ledger command quick reference.
- Evidence storage rule.
- Relationship between ledger, logbooks, specs, and plans.

## 5. Governance Document Contracts

### `docs/governance/root-entry-responsibility-matrix.md`

Include:

- Table of root files.
- What each owns.
- What each must not own.
- Update trigger.
- Verification anchor.

### `docs/governance/documentation-governance-standard.md`

Include:

- One-fact-one-source rule.
- Document lifecycle: draft, active, superseded, archived.
- Required frontmatter or header pattern if used.
- Index update rules.
- Log update rules.
- Anti-drift rules.

### `docs/governance/engineering-guardrails.md`

Include:

- Worktree and user-change safety.
- Testing and verification expectations.
- Secrets and local key handling.
- Generated file policy.
- Dependency and package-lock policy.
- Database/schema migration policy.
- Release/deploy risk boundary.

### `docs/governance/worktree-and-branch-policy.md`

Include:

- Active worktree naming.
- When to create a new worktree.
- How to integrate old worktree changes.
- How to seal a dirty worktree.
- Commit boundary examples.

### `docs/governance/archive-policy.md`

Include:

- What can be archived.
- What must remain current.
- How to mark superseded docs.
- Rule forbidding historical rewrite unless explicitly requested.

### `docs/governance/secrets-and-access-policy.md`

Include:

- Secret file names and ignore policy.
- No-print/no-commit rule.
- Where secret templates live.
- Rotation or exposure response.
- SSH and server access rules.

## 6. System Document Template

Every `docs/systems/<system>/README.md` should use this structure:

```markdown
# <System Name>

## Purpose
[what the system does]

## Ownership
[code owners or logical owner, canonical files]

## Runtime Shape
[processes, routes, workers, queues, ports, deploy env]

## Interfaces
| Interface | Direction | Contract | Auth/Permission | Verification |
| --- | --- | --- | --- | --- |

## Data Model
[tables, files, storage keys, important schemas]

## Permissions
[roles, groups, access checks]

## Failure Modes
[known errors, fallbacks, retry/cancel behavior]

## Verification
[commands, tests, manual checks]

## Change Log
[short links to relevant specs/plans/logs]
```

Use `docs/systems/interface-documentation-template.md` for API/provider/interface-specific docs:

```markdown
# <Interface Name>

## Contract Summary
## Request Shape
## Response Shape
## Error Shape
## Auth And Permissions
## Rate Limits And Runtime Limits
## Idempotency And Retry
## Observability
## Test Fixtures
## Compatibility Notes
```

## 7. Frontend Visual Standards

Create `docs/systems/frontend/frontend-design/design-tokens.md`.

Required token categories:

- Colors: page background, panel, elevated panel, border, text primary, text secondary, muted, accent, danger, warning, success, focus ring.
- Typography: font families, sizes, weights, line heights for canvas labels, node titles, parameter labels, hints, buttons, menus.
- Spacing: 2/4/6/8/10/12/16/20/24/32 scale and when to use each.
- Radius: node shell, inner card, controls, pills, menus, dialogs.
- Shadow/elevation: canvas node, selected node, menu, modal.
- Icons: size, stroke, optical alignment, text gap, disabled opacity.
- Ports/connectors: diameter, stroke, hover, active, disabled, label alignment.
- Motion: duration, easing, allowed transitions, reduced-motion behavior.
- Density: minimum row height, section gap, max label width, adaptive node height rule.

Concrete example format:

```markdown
| Token | Value | Usage |
| --- | --- | --- |
| node.radius.outer | 18px | Main canvas node shell |
| node.header.height.min | 44px | Node title/workflow selector band |
| control.icon.size | 16px | Inline buttons and dropdown prefix icons |
```

Create `visual-component-registry.md`.

Each visual component entry must include:

- Component name.
- Purpose.
- Anatomy.
- Tokens used.
- States.
- Accessibility.
- Do not duplicate with.
- Source files or intended source files.

Minimum visual components:

- Node shell.
- Node header.
- Node section.
- Parameter row.
- Port group.
- Runtime/status card.
- Output preview.
- Context menu action.
- Dropdown/select trigger.
- Empty/error/loading state.

Create `functional-component-registry.md`.

Each functional component entry must include:

- Capability name.
- Inputs.
- Outputs.
- Permission boundary.
- Runtime dependency.
- Reuse rule.
- Existing implementation link.
- Verification.

Minimum functional components:

- Provider/workflow selector.
- Machine/instance selector.
- Exposed parameter editor.
- Run controls.
- Output mapper.
- Permission gate.
- Upload/import action.
- Save-to-library action.
- Error normalization.

Create `node-composition-patterns.md`.

Required patterns:

- Provider workflow node.
- Utility transform node.
- Media input node.
- Media output node.
- Admin-configured runtime node.

Each pattern must define header layout, body sections, port behavior, adaptive height rules, empty/error states, and what must be configured in admin instead of canvas.

## 8. Admin Visual Standards

Create `docs/systems/admin/frontend-design/design-tokens.md`.

Required token categories:

- Layout: sidebar width, content max width, page padding, section gap.
- Panels: background, border, radius, shadow, header/body padding.
- Tables: row height, header height, cell padding, typography, selected/hover states.
- Forms: label width, input height, help text, validation message, required mark.
- Drawers/dialogs: width presets, padding, footer actions.
- Status: status pill colors, icon sizes, severity mapping.
- Density modes: default and compact.

Create `component-library-policy.md`.

Required sections:

- Chosen component library or "current in-house system".
- Why it fits the project.
- Theme mapping to tokens.
- Allowed adoption boundary.
- Migration policy.
- Components not to introduce.
- Accessibility requirements.

Create admin visual and functional registries with the same schema as frontend.

Minimum admin visual components:

- Page shell.
- Sidebar/nav item.
- Workspace band.
- Data panel.
- Filter bar.
- Table.
- Form panel.
- Drawer.
- Confirm dialog.
- Status pill.
- Save bar.

Minimum admin functional components:

- Permission matrix.
- User/group selector.
- Provider/workflow mapper.
- Upload dropzone.
- Task log table.
- Metric card.
- Audit event viewer.
- Release/environment status block.

## 9. Logbook Contracts

In lightweight mode, logbooks are the primary audit evidence. In ledger mode, logbooks are supplemental; the ledger owns task status and evidence records.

Daily log entry structure:

```markdown
# YYYY-MM-DD

## Intent
[why work happened]

## Changed
| Area | Files | Purpose |
| --- | --- | --- |

## Verification
| Check | Result | Notes |
| --- | --- | --- |

## Decisions
[durable choices made]

## Risks
[known gaps, follow-ups]

## Next
[specific next action]
```

Release log entry structure:

```markdown
# Release <version> - <environment>

## Scope
## Commits
## Migration
## Verification
## Rollback
## Incidents
## Final State
```

Incident log entry structure:

```markdown
# Incident <date> - <title>

## Impact
## Detection
## Timeline
## Root Cause
## Fix
## Prevention
## Follow-up Verification
```

## 10. Specs And Plans

Spec files should answer what and why.

Required spec sections:

- Problem.
- Goals.
- Non-goals.
- Users and permissions.
- Current behavior.
- Proposed behavior.
- Data/API contracts.
- UI/UX requirements if relevant.
- Acceptance criteria.
- Risks and open questions.

Plan files should answer how and when.

Required plan sections:

- Preconditions.
- Phase list.
- Touched files per phase.
- Verification per phase.
- Rollback path.
- Log/update requirements.
- Completion checklist.

Do not put hidden implementation decisions only in chat. Durable choices belong in specs, plans, ADRs, or system docs.

## 11. Verification Scripts

Prefer small deterministic scripts that check stable anchors. They should:

- Fail with actionable messages.
- Avoid checking brittle prose wording.
- Avoid network or production mutation.
- Be runnable locally.
- Be wired into aggregate package scripts when possible.

Useful scripts:

- `verify-documentation-entry-contract`: root entries link to canonical docs and avoid duplicate current-state ownership.
- `verify-visual-design-docs-contract`: frontend/admin design docs exist and contain required anchors.
- `verify-design-token-docs-contract`: token docs contain concrete value tables.
- `verify-component-registry-docs-contract`: visual and functional registries contain required component sections.
- `verify-system-doc-template-contract`: systems docs include purpose/interfaces/data/runtime/permissions/verification sections.
- `verify-harness-doc-sync-contract`: package scripts and harness docs mention the same aggregate commands.
- `verify-release-entry-consistency`: release index, ops current, README, and memory agree on environment/version state.
- `verify-secret-ignore-contract`: known local key names and secret patterns are ignored and not tracked.
- `verify-ledger-contract`: in ledger mode, required ledger files exist, generated database is ignored, required tables exist, and evidence paths resolve.

Package script pattern:

```json
{
  "scripts": {
    "harness:verify:project": "npm run verify:documentation-entry-contract && npm run verify:visual-design-docs-contract && npm run verify:component-registry-docs-contract",
    "harness:verify:workspace": "npm run type-check && npm run verify:package-exports",
    "harness:verify:release": "npm run verify:release-entry-consistency && npm run verify:release-worktree-clean"
  }
}
```

Adapt commands to the actual stack. Do not invent package commands without creating the scripts or documenting them as planned.

Ledger mode command pattern:

```bash
bin/harness ledger init
bin/harness ledger create-task --title "<task>"
bin/harness ledger update-task --task-id TASK-... --status in_progress
bin/harness ledger add-decision --task-id TASK-... --content "<decision>"
bin/harness ledger add-evidence --task-id TASK-... --type test --path ledger/evidence/<file>.md
bin/harness ledger add-review --task-id TASK-... --score 8.5 --findings "<findings>"
bin/harness ledger summary
bin/harness verify --write-evidence
```

Do not require these commands in lightweight mode.

## 12. Maintenance Loop

At the start of a task:

- Read `AGENTS.md`, `README.md`, `docs/INDEX.md`, current state, latest daily log, and relevant system docs.
- Run `git status --short`.
- Identify if docs or harness contracts are in scope.
- In ledger mode, run or inspect the ledger summary and create/update the current task.

During a task:

- Update plans/specs before high-risk changes.
- Keep facts in canonical locations.
- Add or update component registry entries before duplicating UI/functional modules.
- Update system docs when interfaces, permissions, runtime, or data flow changes.
- Add verification before relying on manual memory.
- In ledger mode, record important decisions and evidence as the task evolves.

At the end of a task:

- Run relevant harness checks.
- Update daily/validation/release logs in lightweight mode, or ledger evidence plus supplemental logs in ledger mode.
- Update affected indexes.
- Record risks and next step.
- Leave worktree state explicit.
- Commit in small coherent boundaries when requested.

## 12.1 Documentation Impact And User Confirmation

After every meaningful code, configuration, dependency, interface, or
structure change, perform this small review:

1. What project fact changed or may now be stale?
2. Which file is the canonical owner of that fact?
3. Does the current text still match the repository?
4. Classify the result: `no update needed`, `routine record`, `proposed
   authority update`, or `conflict requiring user decision`.

Routine progress, test results, validation evidence, and known risks may be
recorded without interrupting the user. Ask the user before changing
`AGENTS.md`, project purpose or scope, acceptance criteria, architecture,
security or deployment policy, verification gates, or an approved decision.
When code and documentation disagree, present the facts and proposed files; do
not silently choose a source. Record the confirmed decision in the appropriate
decision or logbook file.

Use this impact table as a default:

| Change | Inspect | Default action |
| --- | --- | --- |
| Internal implementation | related system docs and tests | update only if behavior changed |
| Public interface or data model | requirements, systems, decisions | ask before authority update |
| Start/test/build command | README, AGENTS, verification docs | ask if authoritative text changes |
| Permission, secret, or deployment rule | governance and ops docs | always ask |
| Confirmed progress or test result | current state and logbook | routine record |

## 12.2 Optional Tool Protocols

CodeGraph and RTK are Codex aids, not project dependencies. If detected,
record their availability in the Harness adoption or validation report rather
than hard-coding a machine path or version into `AGENTS.md`.

CodeGraph may be used for unfamiliar modules, cross-file exploration, and
impact analysis. Confirm important findings against current source and tests;
fall back to `rg` and direct inspection when unavailable or stale. It is never
required for setup, build, test, release, or Harness verification.

RTK may compress routine shell output. Verification must remain runnable with
native commands. Use the native command when compact output is incomplete or
diagnosis needs the raw stream. Do not change global RTK hooks as part of
project work without explicit user approval.

## 12.3 Project Workflow Registry

For larger projects, create a local workflow registry. These are project-local
governance procedures that Codex can follow; they do not create or configure a
new Agent runtime.

Recommended registry entries:

- `setup-governance-harness`: initialize or repair root entries, docs, verification, and optional ledger.
- `migrate-existing-project`: adopt harness gradually without deleting legacy docs.
- `maintain-docs-architecture`: keep routes, sources of truth, indexes, and archive state healthy.
- `update-visual-standards`: maintain design tokens and component registries.
- `run-harness-verification`: run checks, write reports, and attach evidence.
- `manage-ledger`: create/update tasks, decisions, evidence, reviews, costs, and visual changes.
- `plan-fullstack`: plan cross-stack features before implementation.
- `implement-frontend`: implement UI under visual/component rules.
- `implement-backend`: implement APIs and runtime changes under system contracts.
- `review-and-evidence`: review changes and produce durable findings.
- `operate-long-running-project`: periodic cleanup, drift checks, and archival.

Use this registry when a project needs repeatable project procedures but does not
need every procedure to become a global Codex skill.

## 13. Project Start Checklist

Use this checklist when bootstrapping a new project:

- Project root and active branch are declared.
- Governance mode is selected and recorded.
- `AGENTS.md` exists and names reading order, safety, verification, and logging duties.
- `README.md` explains purpose, setup, architecture, commands, docs map, and current state pointer.
- `docs/INDEX.md` routes every major doc family.
- Governance docs define root responsibility, documentation rules, engineering guardrails, worktree policy, archive policy, and secrets policy.
- System template exists when the project has multiple systems.
- Frontend/admin design token docs and component registries exist when the project has a UI.
- Logbook folders and a current entry exist when the project uses ongoing audit records.
- Requirements and plans exist when the project has approved scope or multi-step work.
- Verification scripts or planned verification contracts exist for every material rule.
- Package scripts or equivalent commands expose harness verification.
- If ledger mode is active, ledger files exist, generated DB is ignored, CLI works, and verification can write evidence.

## 14. Common Failure Modes

| Failure | Prevention |
| --- | --- |
| `AGENTS.md` becomes a diary | Keep it as constitution; move history to logbooks |
| `README.md` duplicates system docs | Summarize and link to canonical system files |
| Visual docs use adjectives only | Require token tables with exact values |
| Component registry becomes a wish list | Require source links, reuse rules, states, and verification |
| Logs are skipped after changes | Make log update part of completion checklist |
| Verification commands are invented but not implemented | Add script first or mark command as planned |
| Historical docs are rewritten accidentally | Use archive policy and superseded markers |
| AI agents keep making one-off UI | Require registry lookup before new component work |
| Ledger and markdown logs disagree | Pick one canonical task-status source; make the other supplemental |
| Heavy harness slows small project | Use lightweight mode and defer ledger |
| Template is copied without adaptation | Record mode decision, project-specific roots, commands, and ignore rules first |

## 15. Handoff To Other Skills

After this skill completes the harness:

- Use planning skills to write implementation plans.
- Use TDD or diagnosis skills for feature and bug work.
- Use review skills for code review.
- Use QA skills for browser and product checks.
- Use release/deploy skills for gray and production rollout.
- Use design implementation skills for actual UI build work.
