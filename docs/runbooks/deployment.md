# Publish and upgrade consumers

cron ships as a versioned Go module. Production deployment belongs to consuming applications; this repository has no release-on-merge workflow.

1. Run [verification](../development/testing.md) and review parser, time-zone, overlap and lifecycle compatibility.
2. Merge the approved change to `master` and verify the resulting CI run. Select an unused semantic version and create a new immutable `vX.Y.Z` tag on the reviewed `origin/master` commit, then push that tag.
3. Update a consumer with `go get github.com/nanostack-dev/cron@vX.Y.Z` and `go mod tidy`; review its module files and test schedule acceptance, next activations and shutdown behavior.
4. Deploy through the consumer's runbook. Verify scheduler registration and the application's observed execution evidence; a next-activation snapshot alone does not prove successful job completion.

Preserve existing tags. Document public compatibility changes and link companion consumer PRs. A docs-only merge runs CI but does not create a new package tag automatically.
