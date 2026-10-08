# Local setup

Clone this repository independently and use the Go version declared by [go.mod](../../go.mod), currently 1.26.5 or newer. No database, Docker, sibling repository or shared workspace is needed.

```sh
go mod download
go test ./...
go build ./...
```

The module currently has no third-party dependencies. Time-zone tests need the host's normal zoneinfo data. To explore the API in a consumer, import `github.com/nanostack-dev/cron` and use the expression/lifecycle examples in the [README](../../README.md).

The default branch is `master`; fetch it before creating an isolated worktree. Keep editor files and temporary experiments out of the documentation PR.
