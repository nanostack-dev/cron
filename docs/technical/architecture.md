# Architecture

cron is a Go library embedded in consuming processes. It is a maintained fork of robfig/cron with the module identity in [go.mod](../../go.mod); it has no independent service or database.

| Area | Responsibility | Coverage |
| --- | --- | --- |
| [parser.go](../../parser.go) | Field selection, descriptors and expression validation | [Parser tests](../../parser_test.go) |
| [spec.go](../../spec.go) | Calendar and time-zone next-activation calculations | [Calendar tests](../../spec_test.go) |
| [constantdelay.go](../../constantdelay.go) | Interval schedules | [Interval tests](../../constantdelay_test.go) |
| [cron.go](../../cron.go) | Entry registration/removal, timer loop and asynchronous invocation | [Lifecycle tests](../../cron_test.go) |
| [chain.go](../../chain.go) | Explicit panic and overlap handling wrappers | [Wrapper tests](../../chain_test.go) |
| [option.go](../../option.go) | Parser, time zone, chain and logger configuration | [Option tests](../../option_test.go) |

## Scheduling contract

The default parser uses five fields beginning with minutes. Seconds are opt-in through `WithSeconds` or a custom parser; a Quartz year field is unsupported. An instance defaults to `time.Local`; `WithLocation` sets its default time zone, and an expression may name `CRON_TZ`.

`Start` begins scheduling, while `Run` blocks in the scheduler loop. A due entry launches its job in a goroutine; later activations can overlap. `DelayIfStillRunning` serializes a wrapped job, `SkipIfStillRunning` skips overlap, and `Recover` explicitly handles panics. The constructor installs an empty chain, so panic recovery is not enabled automatically despite an older source comment describing it.

`Stop` prevents future scheduling and returns a context whose completion waits for running jobs. It does not cancel the jobs themselves. Applications must provide their own cancellation and shutdown limits.

## Durability boundary

Entries and activation state are in memory. Restarting loses them unless the application reconstructs them; separate replicas schedule independently. Missed work, idempotency, retries and distributed uniqueness are consumer responsibilities. Use a durable database-backed scheduler or queue when those semantics are required; cron parsing alone does not supply them.
