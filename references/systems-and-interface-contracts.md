# Systems And Interface Contracts

Each docs/systems/<system>/README.md should document:

1. Purpose and ownership.
2. Runtime shape: processes, routes, workers, queues, ports, and environments.
3. Interfaces with direction, contract, auth/permission, and verification.
4. Data model and important schemas.
5. Permissions and access checks.
6. Failure modes, retries, cancellation, and fallbacks.
7. Verification commands and a short change-log pointer.

Interface-specific documents should additionally cover request/response/error shapes, authentication, limits, idempotency/retry, observability, fixtures, and compatibility notes. Keep one contract authoritative and link to code/tests rather than copying implementation.

Add system folders only for systems that exist. Do not create speculative architecture.
