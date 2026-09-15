# Root And Authority Contracts

## Authority Map

| Fact | Canonical source |
| --- | --- |
| Agent rules and reading order | AGENTS.md |
| Purpose, setup, architecture summary | README.md |
| Documentation routes and ownership | docs/INDEX.md |
| Long-term goals and non-goals | docs/requirements/product-goals.md |
| Phase scope and constraints | docs/requirements/scope.md |
| Acceptance conditions | docs/requirements/acceptance-criteria.md |
| Current phase, risks, next action | docs/current-state.md |
| System behavior and interfaces | docs/systems/<system>/ |
| Durable rationale | docs/decisions/ |
| Approved execution | docs/plans/ or docs/superpowers/plans/ |
| Historical evidence | docs/logbooks/ |
| Verification evidence | docs/validations/ |

## Root File Rules

AGENTS.md contains identity, bounded reading order, safety, worktree, editing, verification, logging, stop-and-ask, and documentation-maintenance rules. It must not contain release history or secrets. README.md contains purpose, setup, architecture, real commands, deployment summary, and links. docs/INDEX.md is a router and source-of-truth table. docs/current-state.md is a short volatile snapshot. Requirements describe approved intent; plans describe how; logs prove what happened.

## Documentation Impact

After meaningful changes identify changed facts, locate canonical owners, and classify: no update needed, routine record, proposed authority update, or conflict requiring user decision. Record routine evidence automatically. Ask before changing purpose, scope, acceptance, architecture, security/deployment policy, verification gates, or approved decisions. Never silently resolve conflicts.
