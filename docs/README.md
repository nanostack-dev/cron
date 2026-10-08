# cron documentation

Start with [agent rules](../AGENTS.md), [canonical vocabulary](../CONTEXT.md) and the [public API/migration guide](../README.md).

- [Architecture](technical/architecture.md): parser, scheduler lifecycle, wrappers and durability boundaries.
- [Setup](development/setup.md), [testing](development/testing.md), [troubleshooting](development/troubleshooting.md).
- [Module publishing and consumer upgrades](runbooks/deployment.md), [rollback](runbooks/rollback.md).
- [Architectural decisions](adr/README.md).

[doc.go](../doc.go) contains the upstream-style package reference; the current [go.mod](../go.mod) owns the supported toolchain. Keep application-specific schedule behavior in the consumer. Add research or postmortems when actual findings or incidents warrant them.
