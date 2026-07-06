# Project Harness Governance

`project-harness-governance` is a Codex skill for creating and maintaining the operating layer around medium and large software projects.

It helps an AI coding agent establish the durable project rules, documentation architecture, visual standards, component registries, verification contracts, and audit trail that keep long-running work from dissolving into chat memory.

## What Problem This Solves

Large AI-assisted projects often fail in the same quiet ways:

- The agent no longer knows which worktree, branch, or environment is current.
- `README.md`, `AGENTS.md`, daily logs, and plans all describe different states.
- Feature work starts before project rules, verification, or source-of-truth boundaries are clear.
- Frontend and admin UI styles drift because there is no design token or component registry.
- Future agents repeat previous mistakes because decisions and evidence stayed in chat.
- Release and gray-production workflows become hard to reproduce.

This skill gives the agent a repeatable harness-building workflow before feature implementation begins.

## What The Skill Creates Or Repairs

The skill guides the agent to build a project governance layer such as:

- `AGENTS.md` as the agent constitution.
- `README.md` as the human project overview.
- `docs/INDEX.md` as the documentation router.
- `docs/governance/` for durable engineering and documentation rules.
- `docs/systems/` for system contracts, interfaces, runtime shape, data flow, permissions, and verification.
- `docs/logbooks/` for audit evidence.
- `docs/superpowers/specs/` and `docs/superpowers/plans/` for design and execution records.
- Frontend and admin visual design standards with concrete design tokens.
- Visual and functional component registries to reduce duplicate UI and duplicate logic.
- Verification scripts or contract checks for stable project anchors.
- Optional Ledger/CLI mode for projects that need queryable task, decision, evidence, review, cost, and visual-change records.

The skill does not implement product features, run deployments, or replace code review. It prepares the governance layer that makes those later steps safer.

## When To Use It

Use this skill when:

- Starting a new medium or large project.
- Converting a prototype into a long-running codebase.
- Restructuring a project whose docs, plans, logs, and current state have drifted.
- Preparing a project for repeated AI-agent collaboration.
- Creating an `AGENTS.md` constitution and project harness.
- Defining frontend/admin visual standards and reusable component registries.
- Adding verification contracts for docs, release state, package exports, or project entry files.
- Migrating from ad hoc chat-driven work into auditable project execution.

Do not use it for:

- A single small script.
- Direct feature implementation.
- Debugging a specific runtime bug.
- UI implementation after the design system already exists.
- Release/deployment execution.

## Installation

Clone this repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/Hhh2178/project-harness-governance.git ~/.codex/skills/project-harness-governance
```

On Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force $env:USERPROFILE\.codex\skills | Out-Null
git clone https://github.com/Hhh2178/project-harness-governance.git $env:USERPROFILE\.codex\skills\project-harness-governance
```

If the folder already exists:

```bash
cd ~/.codex/skills/project-harness-governance
git pull
```

## Usage

In Codex, ask for the skill explicitly:

```text
Use $project-harness-governance to establish the harness, documentation, visual standards, and verification structure for this project.
```

Example prompts:

```text
Use $project-harness-governance to create a project harness for this existing repo. Start by auditing the current root files and docs.
```

```text
Use $project-harness-governance to repair our AGENTS.md, README, docs index, system docs, logbooks, and verification contracts.
```

```text
Use $project-harness-governance to design the frontend and admin visual standards, design tokens, and component registries before new UI work starts.
```

```text
Use $project-harness-governance to decide whether this project needs lightweight doc-log mode or Ledger mode.
```

## Governance Modes

The skill supports two governance modes.

### Lightweight Doc-Log Mode

This is the default. It is best for most projects.

It uses:

- Markdown documentation.
- `docs/logbooks/` for audit history.
- Specs and plans for durable decisions.
- Verification scripts or package commands for project checks.

Choose this when the project needs clarity and auditability without adding a local database or CLI.

### Ledger Mode

Ledger mode is optional and heavier.

Use it when the project is long-running, multi-agent, high-audit, or high-risk and needs queryable records for:

- Tasks.
- Decisions.
- Evidence.
- Reviews.
- Costs.
- Visual changes.

In Ledger mode, the ledger owns task status and evidence. Markdown logbooks become supplemental narrative records. The skill intentionally does not force Ledger mode into every project.

## Repository Structure

```text
project-harness-governance/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── harness-blueprint.md
```

`SKILL.md` is the compact triggerable skill body.

`references/harness-blueprint.md` contains the detailed templates and contracts for:

- Project start procedure.
- Governance mode selection.
- Starter file tree.
- `AGENTS.md` constitution.
- `README.md` and docs index responsibilities.
- Governance document contracts.
- System document templates.
- Frontend/admin visual design standards.
- Visual and functional component registries.
- Logbook, spec, and plan templates.
- Verification script ideas.
- Optional Ledger mode structure.
- Maintenance loop and common failure modes.

## Expected Workflow

When the skill is used, the agent should:

1. Inspect the project state and current worktree.
2. Classify existing changes before editing.
3. Choose lightweight doc-log mode or Ledger mode.
4. Establish root authority through `AGENTS.md`, `README.md`, and `docs/INDEX.md`.
5. Create or repair governance, system, logbook, spec, and plan structure.
6. Define frontend/admin visual standards and component registries.
7. Add verification contracts where practical.
8. Record audit evidence.
9. Leave the worktree state explicit.

## Design Principles

- One fact has one canonical source.
- Root files summarize and link; they do not hold long histories.
- Governance docs explain rules.
- System docs explain how systems work.
- Logbooks or Ledger prove what happened.
- Visual standards must include concrete values, not only adjectives.
- Component registries must separate visual components from functional modules.
- Verification scripts should check stable anchors, not brittle prose.
- Documentation is not a substitute for automated checks when checks are practical.

## Validation

This skill has been validated with the Codex skill validator:

```bash
python ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ~/.codex/skills/project-harness-governance
```

Expected result:

```text
Skill is valid!
```

## License

MIT. See `LICENSE`.
