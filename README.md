# Project Harness Governance

`project-harness-governance` is a Codex skill for establishing and maintaining a durable governance layer inside an existing project repository. It keeps project intent, current state, working rules, verification contracts, and audit evidence easy to find across long-running Codex sessions.

The skill creates a project harness; it does not create an Agent, orchestration service, context database, product feature, or deployment platform.

## Why Use It

AI-assisted projects lose continuity when branch state, requirements, plans, logs, and verification results live in different places. This skill gives the repository explicit ownership boundaries so Codex can resume work without relying on chat history or guesswork.

Core principles:

- One fact has one canonical source.
- `AGENTS.md` is the project constitution, not a diary.
- `README.md` is a concise human entry point.
- `docs/INDEX.md` routes to the relevant requirements, systems, plans, decisions, and logs.
- Current state stays short and volatile; history stays append-only in logs or a ledger.
- Verification remains runnable with the project’s native toolchain.
- Changes to authority documents require user confirmation when code and documentation disagree.

## What It Establishes

Depending on project size and risk, the skill creates or repairs:

- `AGENTS.md`, `README.md`, and `docs/INDEX.md`
- Requirements, scope, acceptance criteria, and current-state records
- Governance policies for documentation, worktrees, secrets, releases, and archival
- System and interface contracts for frontend, backend, workers, providers, storage, and operations
- Specs, implementation plans, daily logs, validation evidence, release records, and incident records
- Frontend/admin design tokens and visual/functional component registries when a UI exists
- Small deterministic harness checks for documentation, commands, exports, secrets, and release consistency
- Optional Ledger mode for queryable tasks, decisions, evidence, reviews, costs, and visual changes

The generated structure is adapted to the repository. Small projects stay small; Ledger and extra document families are added only when their operational value justifies the maintenance cost.

## When To Use It

Use this skill when starting or restructuring a project that needs durable Codex guidance, clear document ownership, requirements and acceptance records, current-state tracking, verification contracts, or an auditable work log. It is also useful when existing `README.md`, `AGENTS.md`, plans, and logs have drifted.

Do not use it as a replacement for feature implementation, debugging, product QA, code review, or release execution.

## Quick Start

Install the skill into the Codex skills directory:

```powershell
New-Item -ItemType Directory -Force $env:USERPROFILE\.codex\skills | Out-Null
git clone https://github.com/Hhh2178/project-harness-governance.git $env:USERPROFILE\.codex\skills\project-harness-governance
```

To update an existing installation:

```powershell
git -C $env:USERPROFILE\.codex\skills\project-harness-governance pull
```

Then ask Codex:

```text
Use $project-harness-governance to audit this repository and establish the smallest appropriate project harness.
```

The skill starts by inspecting the worktree and existing documentation, records the governance mode decision, and asks before changing project authority when confirmation is required.

## Governance Modes

### Lightweight doc-log mode

The default for most projects. It uses Markdown requirements, plans, system docs, `docs/logbooks/`, and native project verification commands. It adds clarity and auditability without a local database or CLI.

### Ledger mode

An optional heavier model for long-running, multi-agent, high-audit, or high-risk repositories. A local ledger owns task status and structured evidence; Markdown logs remain supplemental narrative. It is never enabled solely because the skill is installed.

## Optional Codex Tools

The harness may document two optional local aids when they are available:

- **CodeGraph**: repository navigation and cross-file impact analysis. Findings must be checked against current source and tests; `rg` and direct inspection are the fallback.
- **RTK**: shell-output compression for routine commands. Native commands remain the verification source, and global hooks are never changed without explicit approval.

Neither tool is a product dependency or a prerequisite for building, testing, releasing, or verifying a project harness.

## Repository Layout

```text
project-harness-governance/
├── SKILL.md                         # Compact triggerable guidance
├── references/harness-blueprint.md  # Reference index and reading routes
├── references/                      # Task-scoped governance contracts
├── agents/openai.yaml               # Codex display metadata
└── LICENSE
```

Read `SKILL.md` for the operating workflow, then use `references/harness-blueprint.md` as a routing index. Follow only the task-scoped reference you need: lifecycle/modes, root authority, systems/interfaces, UI standards, evidence/verification, or Ledger/optional tools. This keeps routine Codex work focused and reduces context cost.

## Validation

Run the Codex skill validator before publishing changes:

```powershell
python $env:USERPROFILE\.codex\skills\.system\skill-creator\scripts\quick_validate.py .
```

## License

MIT. See [LICENSE](LICENSE).
