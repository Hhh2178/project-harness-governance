# Ledger And Optional Tools

## Ledger Mode

Use only when the project needs queryable structured history. A local ledger may own tasks, decisions, evidence, reviews, costs, and visual changes; Markdown logs become supplemental narrative. Typical capabilities are setup/init, create/update task, add decision/evidence/review, summary, and verification with evidence output. Generated database state must be ignored by git.

## CodeGraph

Optional navigation for unfamiliar repositories, structural exploration, and cross-file impact analysis. Confirm important findings against current source and tests. Fall back to rg, language tooling, and direct inspection when unavailable or stale.

## RTK

Optional shell-output compression for routine commands. Native commands remain the verification source. Use raw native output when compact output is incomplete or diagnosis needs it. Never change global hooks as project work without explicit user approval.

Neither CodeGraph, RTK, nor Ledger is a product dependency or prerequisite for setup, build, test, release, or Harness verification.
