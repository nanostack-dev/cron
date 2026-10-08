# cron context

cron interprets calendar expressions and schedules jobs within one process. Applications own persistence and coordination across replicas.

## Language

**Cron expression:** A textual selection of activation times, using the configured parser's fields, descriptors and time zone.

**Schedule:** A rule that computes the next activation strictly after a supplied time.

**Entry:** One registered job and schedule, with a scheduler-local identity and previous/next activation snapshots.

**Job:** The action invoked when an entry activates. A job is separate from a durable queue job in pgkit.

**Job wrapper:** Behavior around a job invocation, such as explicit panic recovery or overlap handling.

**Chain:** An ordered composition of job wrappers applied to a registered job.

**Activation:** A schedule becoming due for one entry. It does not imply the job completed successfully.
