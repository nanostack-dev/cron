# Local setup

Clone this repository independently and use the Go version declared by [go.mod](../../go.mod), currently 1.26.5 or newer. No database, Docker, sibling repository or shared workspace is needed.

```sh
go mod download
go test ./...
go build ./...
```

The module currently has no third-party dependencies. Time-zone tests need the host's normal zoneinfo data. To explore the API in a consumer, import `github.com/nanostack-dev/cron` and use the expression/lifecycle examples in the [README](../../README.md).

The default branch is `master`; fetch it before creating an isolated worktree. Keep editor files and temporary experiments out of the documentation PR.

## Agent clients

Codex, OpenCode and Grok Build read the local `AGENTS.md` directly. Claude Code loads it through the committed [.claude/settings.json](../../.claude/settings.json) SessionStart hook, which resolves the Git root and prints that guide using only Git and the shell. Start from this repository or a nested directory.

Approve repository trust through the client when required, and start a new session after changing hooks or installed skills so the client reloads them. Trust and login are developer-controlled. Keep personal overrides in ignored `.claude/settings.local.json`; no shared-workspace checkout or external skill installer is required.
