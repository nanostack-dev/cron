# Development troubleshooting

## A six-field expression is rejected

The default parser expects five fields beginning with minutes. Use `WithSeconds()` when the first seconds field is required, or `WithParser(...)` with `SecondOptional` when it is optional. Validate with `AddFunc`/`AddJob` error handling and the [parser tests](../../parser_test.go); the year field is unsupported.

## An entry runs in an unexpected time zone

The instance defaults to `time.Local`. Set `WithLocation(...)` explicitly or use the supported `CRON_TZ` expression prefix. Inspect the entry's next activation and rerun [time-zone tests](../../spec_test.go). Calendar schedules are subject to daylight-saving transitions; interval schedules have different semantics.

## Jobs overlap or shutdown returns before a handler completes

Jobs run asynchronously and overlap by default. Choose `DelayIfStillRunning` or `SkipIfStillRunning` when the application needs a different overlap policy. On shutdown, wait for the context returned by `Stop`; it does not cancel running jobs. Verify with [wrapper](../../chain_test.go) and [stop-and-wait](../../cron_test.go) coverage.

## A job panic crashes the process

The default chain is empty. Configure `WithChain(Recover(logger))` when recovery is the desired application policy, despite an older constructor comment suggesting automatic recovery. Confirm the chosen policy against [panic tests](../../cron_test.go).

Keep verified repairs here; unresolved hypotheses belong in an issue or research document.
