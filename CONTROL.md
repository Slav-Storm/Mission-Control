# Validated local objectives — command loop v1

Mission Control now accepts **SURVEY_AREA**, a bounded horizontal inspection survey
that retraces its route and returns to its starting pose. No digging, item use or
arbitrary turtle instructions are exposed. Other strategic operations remain planned.
`status` remains a read operation rather than a robot job.

The executable source remains in the local installation; this public repository is
documentation-only.

## Submit and inspect

Run from the local project root with Node on PATH:

```powershell
node viewer/agent.mjs snapshot
node viewer/agent.mjs draft 1 > survey.json
node viewer/agent.mjs submit survey.json
node viewer/agent.mjs command COMMAND_UUID
node viewer/agent.mjs commands --status active
node viewer/agent.mjs commands --status COMPLETED
node viewer/agent.mjs commands --status REJECTED
node viewer/agent.mjs commands --status FAILED
```

`draft` creates a UUID and five-minute expiry. It does not submit. Its optional
second argument is a JSON parameters object. Survey bounds are relative to the
chosen robot's actual accepted pose: `radius` 1–16, `limit` 2–64 visited cells and
`vertical` exactly 0. Default parameters are radius 4 and limit 16. Mission Control
selects the existing `area_survey` implementation and owns its job creation.

Preserve the original envelope when retrying. An identical ID and payload returns
the original transport receipt without another job. A changed payload under the
same ID receives `ID_REUSE_CONFLICT`. To express a new objective, create a new ID.

A `SUBMITTED` CLI response means durable delivery to the input spool only. The
command becomes authoritative when Mission Control records it. Querying before
that may report that the ID is not yet recorded. Check `sourceOK`, `lastRead` and
robot radio timestamps; a paused game cannot validate or execute pending commands.
Do not interpret a cached result as fresh just because HTTP returned successfully.

## Boundaries and storage

The CLI imports `command-transport.mjs` only for `submit`. It flushes a temporary
file, closes it and atomically creates an immutable UUID-named request with a hard
link. Exclusive destination creation prevents concurrent retries overwriting an ID.
This requires a filesystem supporting hard links (tested on the installed Windows
filesystem); unsupported filesystems fail instead of falling back to an unsafe write.

Requests reside in computer 0's `commands/inbox/`. They are software input, not
invented Minecraft observations or items. Mission Control owns all authoritative
records in the existing `data/colony.json`: `commands`, `jobs` and `commandPolicy`.
The same atomic store used by the colony persists these records together.
Do not edit authoritative records or completed request files to recover a job.

There is **no command HTTP endpoint**. The local bridge remains GET/HEAD-only and
its WebSocket remains receive-only. The command transport module is not in the
static-file allowlist and is never imported by the server or viewer. Browser
closure, bridge failure and Codex disconnects do not stop accepted robot jobs.
The trusted boundary is the local OS user with write access to this command spool;
it does not isolate a malicious process already running as that user.

## Validation and lifecycle

Mission Control independently validates the complete envelope, operation, expiry,
recorded bootstrap seal, real robot identity, fresh telemetry, idle state, resolved
pose, reported survey capability, fuel, task ownership and known hazards in bounds.
The initial survey requires `2 * (limit - 1) + 64` fuel: a conservative traversal
and return budget plus reserve. This read-only survey does not require mining tools,
recipe inputs or storage space. The worker still inspects adjacent moves and refuses
obstructed returns; unknown terrain is never assumed safe by an external mapper.

Lifecycle:

1. `SUBMITTED`: Mission Control durably records the request and canonical payload.
2. `VALIDATING`: validation begins; interruption can resume before physical work.
3. `ACCEPTED`: the reservation and deterministic child job are committed together.
4. Dispatch rechecks safety, ownership, expiry and unchanged origin. A durable send
   intent is recorded before the existing scheduler sends the job.
5. `RUNNING`: actual worker acknowledgement establishes execution.
6. `COMPLETED`: the worker reports a completed job, a bounded survey result and
   observations, with its final pose and heading equal to the accepted origin.
7. `REJECTED` or `FAILED`: validation or execution fails with a structured reason.

Successful evidence includes the child job and robot IDs, original and final poses,
visited-cell report, observed movement, reported observations, newly known cells,
source/receipt timestamps and Minecraft day. A survey may legitimately discover
zero new cells; completion means it inspected its bounded area and returned, not
that it found a requested resource or fully covered every cell in the bounds.

Existing manual jobs are included in conflict checks. An accepted objective reserves
its robot from other scheduler jobs. Failed ambiguous execution retains that
reservation until an explicit recovery implementation can reconcile it safely.

## Recovery and events

Command records and lifecycle history survive bridge, CLI and Mission Control
restarts. A restart after a dispatch intent does not automatically resend an
ambiguous physical job. Worker outcomes reconcile known execution. No acknowledgement
within 120 seconds produces `DISPATCH_ACK_UNCERTAIN` with the reservation retained.
Incomplete return evidence similarly fails with `COMPLETION_EVIDENCE_MISSING`.
Worker recovery states remain failures requiring diagnosis, never optimistic success.

This version has no cancellation or automated ambiguous-job recovery command.
Expiry applies before dispatch; it does not terminate a robot already exploring.
Spool files and command history are retained; monitor the computer disk as usage
grows. Archival/retention policy is a later checkpoint, not silent deletion now.

Read records via `/api/v1/state/commands` or the normal full snapshot. The existing
semantic event feed projects persistent history as `COMMAND_SUBMITTED`,
`COMMAND_VALIDATING`, `COMMAND_ACCEPTED`, `COMMAND_STARTED`, `COMMAND_COMPLETED`,
`COMMAND_FAILED` and `COMMAND_REJECTED`. Each contains a stable `commandEventId`
alongside the bridge cursor ID. Intermediate lifecycle transitions survive polling
because they are stored by Mission Control. On a new bridge generation, take a
fresh snapshot; command history remains available even if old feed events expired.

General robot actions may still be missed between telemetry samples. The evidence
does not claim a lossless physical trace or an autonomous quest planner. The next
stage should add one bounded production/logistics objective with equally explicit
input validation and delivered-output evidence, using the same scheduler.
