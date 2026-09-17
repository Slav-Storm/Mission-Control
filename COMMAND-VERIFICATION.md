# Headless control loop acceptance — 17 September 2026

The stage passed against the existing Monifactory colony. No Minecraft graphical
input, screenshots, mouse or keyboard were used to submit, execute or verify the
objective. Read-only inspection of the existing browser's visible counters verified
the viewer update; it did not control Minecraft or refresh the page.

## Preservation

An idle-fleet application checkpoint archived all 347 existing ComputerCraft files,
the project sources and an authoritative snapshot, retaining the earlier paused-world
archive. No world was reset, reloaded or restored. Comparison of 205 previously
deployed Lua/config files found exactly one changed existing file: computer 0's
controller. Its new objective library and recorded bootstrap policy were added.
All ten workers retained their software and identities. Existing jobs, discoveries,
storage and production records remained present. A saved-player audit confirmed the
original anchor, survival and cheats disabled; it was not a continuous position sensor.

## One controlled real survey

Codex created a UUID envelope and submitted it using the CLI, then exited that
command interaction. Mission Control recorded:

`SUBMITTED → VALIDATING → ACCEPTED → RUNNING → COMPLETED`

It independently validated Explorer 1, freshness, capability, idle/task ownership,
survey bounds, the bootstrap seal and 158 required fuel units. The accepted survey
used radius 8, at most 48 visited cells and no vertical exploration. The existing
scheduler and unchanged `area_survey` worker performed it.

Authoritative evidence:

- 48 cells visited; 94 movement changes reported to Mission Control.
- Exact return to the original position and heading.
- 40 previously unknown cells added to the authoritative map.
- Completed child job and a retained worker survey report.
- 1,948 reported observations, including knowledge synchronization. This is not
  1,948 unique new discoveries.

An independent receive-only WebSocket witness captured 240 deltas, 88 sampled
position changes and all five lifecycle transitions. Sampling accounts for the
movement-count difference. Its map increased from 9,033 to 9,073 cells and matched
Mission Control, with no keys outside authoritative knowledge. The existing viewer
showed 9,073 mapped cells, ten fresh robots, 174 completed jobs and `+40 discovered`
without refresh. The robot returned idle with 4,008 fuel.

## Rejection and reconnection

After the successful survey, one validly formed envelope targeted an unknown robot.
Mission Control durably returned `REJECTED / UNKNOWN_ROBOT` and created no child job.
No robot was put at risk to test rejection.

At the next idle boundary, Mission Control and the observer bridge were restarted.
Both terminal command records and their evidence survived unchanged. Job count stayed
at 189; Explorer 1 used no additional fuel. Re-submitting the original immutable
envelope returned a duplicate receipt, caused no new job and did not repeat the
survey. The old bridge event cursor correctly required resynchronization with HTTP
409; a fresh snapshot exposed the original command result.

## Automated tests

All 12 Node tests passed, including atomic concurrent submission, ID conflicts,
read-only browser boundaries, lifecycle history projection, snapshots, cursor
reconnection and existing observer behavior. The actual Lua module passed isolated
checks for fuel, radio, capability, ownership, unknown robots, hazards, malformed
inputs, expiry and bootstrap validation; evidence-gated completion; worker failures;
interrupted validation/acceptance/dispatch; and retained recovery reservations.
Existing room-survey and navigation regression checks also passed.

## Resumed progression and limits

After acceptance, another bounded frontier survey was submitted through the validated
interface to continue legitimate exploration. It is a separate progression objective,
not another acceptance-test attempt. The live observer remains running.

This release validates one operation: SURVEY_AREA. It does not claim colony-wide
production planning, automatic quest completion, cancellation or automatic recovery
of ambiguous physical execution. Those capabilities must extend the same lifecycle
and scheduler. See [CONTROL.md](CONTROL.md) for the exact interface and limits.

Detailed command IDs, coordinates, snapshots, raw witness data and restart evidence
are retained only in the local `viewer/runtime/` directory.
