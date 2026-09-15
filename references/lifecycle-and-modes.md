# Lifecycle And Governance Modes

## Start Sequence
1. Inspect git status, root files, docs, manifests, scripts, CI, and recent logs.
2. Classify dirty work as user work, generated output, harness work, or unknown.
3. Identify canonical root, branch, environments, commands, deployment path, secrets policy, and roadmap.
4. Choose lightweight doc-log mode unless queryable records are justified.
5. Repair root entries and routing before adding secondary documents.
6. Add only relevant systems, requirements, plans, logs, and checks.
7. Run verification and record mode, evidence, risks, and next action.

## Mode Selection

| Mode | Use when | Canonical status | Cost |
| --- | --- | --- | --- |
| Lightweight doc-log | Small/medium project or low audit need | Markdown current state and logs | Low |
| Ledger | Multi-agent, high-risk, status drift, searchable evidence, or explicit request | Local ledger | Medium |

Do not enable Ledger merely because the skill is installed. Keep generated databases ignored by git.

## Minimality

Start with AGENTS.md, README.md, docs/INDEX.md, docs/current-state.md, requirements when scope exists, and logbooks when ongoing evidence is needed. Add system, UI, validation, incident, or Ledger folders only when they have an owner and update trigger.

## Maintenance Loop

At task start read the bounded root contract and relevant routed docs. During work update specs before high-risk changes. At task end run checks, record evidence, update current state/indexes, classify documentation impact, and leave worktree state explicit.
