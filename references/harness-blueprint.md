# Harness Blueprint Index

This file is the entry point for the reference set. Read the smallest relevant reference instead of loading the entire set. The Harness is a repository governance layer, not an Agent runtime or project-specific tool platform.

## Reading Routes

| Need | Read | Output |
| --- | --- | --- |
| Start or restructure a project | `lifecycle-and-modes.md` | Mode decision and rollout order |
| Define root files and source of truth | `root-and-authority-contracts.md` | Root entries, docs router, requirements/state |
| Document systems and interfaces | `systems-and-interface-contracts.md` | System and interface contracts |
| Govern UI structure | `frontend-and-admin-standards.md` | Tokens, registries, composition rules |
| Record work and verify the Harness | `evidence-and-verification.md` | Logs, plans, checks, evidence |
| Use Ledger, CodeGraph, or RTK | `ledger-and-optional-tools.md` | Optional structured evidence and tool policy |

## Universal Rules

- Inspect `git status --short` and existing docs before editing.
- Keep one canonical source for each fact.
- Read root entries and current state, then only routed material.
- Adapt the structure to project size; do not create empty ceremony.
- Ask before changing authority documents when code and documentation conflict.
- Keep verification runnable without optional tools.

## Project Start Checklist

- Root, branch/worktree, environments, and existing changes are identified.
- Governance mode is recorded.
- Root entries and docs routing are coherent.
- Requirements, current state, systems, plans, logs, and evidence have distinct owners.
- Relevant deterministic checks run and their results are recorded.
- Risks, next action, and worktree state are explicit.

For detailed contracts, follow the route table above. Do not treat this index as a second source of project facts.
