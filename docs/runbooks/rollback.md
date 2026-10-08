# Roll back a consumer upgrade

1. Identify the previous cron version and any changed consumer parser, time-zone or wrapper options.
2. Restore the earlier compatible version with `go get github.com/nanostack-dev/cron@vPREVIOUS`, run `go mod tidy`, and revert matching caller changes. Run consumer tests and use its deployment rollback procedure.
3. Verify registered entries, next activations, overlap and shutdown behavior after restart. In-memory state is reconstructed by the application; completed external effects cannot be reversed by downgrading the module.
4. Repair or revert the source through a new PR and publish a new version. Keep published tags immutable. Record verified findings in troubleshooting or technical docs, and add a postmortem for a significant incident.
