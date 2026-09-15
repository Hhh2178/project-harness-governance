# Evidence And Verification

## Log Contracts

Daily records contain intent, changed files and purpose, verification results, decisions, risks, and next action. Release records contain scope, commits, migration, verification, rollback, incidents, and final state. Incident records contain impact, detection, timeline, root cause, fix, prevention, and follow-up verification.

## Specs And Plans

Specs answer what and why: problem, goals, non-goals, users/permissions, current and proposed behavior, contracts, acceptance criteria, risks, and open questions. Plans answer how and when: preconditions, phases, touched files, verification, rollback, logging, and completion checklist.

## Deterministic Checks

Prefer local checks for documentation anchors, routing, command consistency, system templates, secret ignores, package exports, release state, and (when enabled) Ledger schema/evidence. Checks must fail clearly, avoid brittle prose and network mutation, and be runnable with native commands.

## Completion

Before declaring Harness work complete: root authority is coherent; requirements, state, plans, and evidence are distinct; relevant checks ran; impact was classified; confirmations were obtained; risks and next action are explicit; and git status is reported.
