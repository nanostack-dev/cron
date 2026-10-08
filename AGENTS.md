# cron agent guide

This is Nanostack's maintained Go cron parser and in-process scheduler fork. Local documentation is sufficient for standalone work; the shared workspace and external skills are optional enhancements.

## Read by task

- Schedule terminology: read [CONTEXT.md](CONTEXT.md).
- Parser, time-zone or lifecycle changes: read [architecture](docs/technical/architecture.md) and the affected source/tests linked there.
- First checkout or local failure: read [setup](docs/development/setup.md) and [troubleshooting](docs/development/troubleshooting.md).
- Code changes: run the checks in [testing](docs/development/testing.md).
- Module release or consumer upgrade: read [deployment](docs/runbooks/deployment.md) and [rollback](docs/runbooks/rollback.md).

## Invariants and delivery

- Preserve the existing cron parsing and next-activation semantics, especially time zones, daylight-saving transitions, seconds options and invalid expressions. Applications own durable schedule state, retries and distributed coordination.
- Jobs execute asynchronously and may overlap by default. Keep panic recovery, skipping or serialization explicit through wrappers; preserve stop-and-wait behavior.
- Keep public compatibility and the module identity explicit. This repository is a maintenance fork; avoid application-specific dependencies or naming.
- Fetch the default branch (`origin/master`) and edit in an isolated worktree; preserve the primary checkout. Use Conventional Commits and open a focused PR after local checks. CI is the final gate. Review requests end with findings and a verdict before implementation.

Update authoritative docs in the same PR when behavior, vocabulary, a verified recurring fix or a consequential choice changes. Current behavior belongs in `docs/technical/`, development repairs in `docs/development/`, release procedures in `docs/runbooks/` and vocabulary in `CONTEXT.md`. ADRs record real alternatives and consequences; preserve numbers and supersede reversals with a new record. Keep [docs/README.md](docs/README.md) current. `AGENTS.md` is the sole agent guide filename.
