# Testing

Run checks from the Go module root. [CI](../../.github/workflows/ci.yml) uses the Go version from `go.mod`, vets the code and runs race-enabled tests.

```sh
go vet ./...
go test -race -count=1 ./...
go build ./...
```

The repository also carries [golangci-lint configuration](../../.golangci.yml); run `golangci-lint run` when changing code. Its upstream-test exclusions are existing constraints, rather than permission to add new suppressions.

Parser changes need invalid-expression, field-option and descriptor cases. Calendar changes need time-zone, leap/calendar boundary and daylight-saving coverage. Lifecycle/wrapper changes need concurrency, entry removal, overlap and stop-and-wait tests. Preserve the maintained fork's public semantics.

Documentation changes need local link validation and `git diff --check`; use existing tests rather than adding tests that only mirror prose. Report exact local and CI results, including skipped or unavailable checks.
