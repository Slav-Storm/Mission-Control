# Verification checkpoint — 17 September 2026

These results describe the tested local implementation at this checkpoint. They
are historical evidence, not a claim that the colony is currently at these counts.
Detailed evidence and coordinates remain local.

## Preservation

A paused-world disk archive, project archive and SHA-256 manifest were created
before observer development. A second source/state checkpoint preceded the headless
extension. The existing world was resumed in place without reset, reload or restore.
Disk checkpoints do not capture running Lua stacks.

All original robot IDs, jobs, map keys, storage keys and production records survived.
Comparison of 205 deployed Lua/config files against checkpoint hashes found no
changes. A saved-player audit confirmed the original anchor, survival mode and
cheats disabled; this was not a continuous live position sensor.

## Live observer acceptance

| Requirement | Observed result |
| --- | --- |
| Existing territory loads | Initial authoritative snapshot rendered 8,666 known cells |
| Fleet positions | All ten existing identities loaded at reported poses; stale radio ages remained visible |
| Movement without refresh | A 100-second witness recorded 31 positional updates and 73 incremental messages |
| Exploration expands the map | The same browser advanced from 8,666 to 8,982 cells without refresh; later observations reached 9,033 |
| Observer isolation | The actual bridge was stopped for 30 seconds while Minecraft time, recording and an existing robot job continued |
| Reconnection | Browser and client recovered through fresh authoritative snapshots without page refresh |
| Only known terrain | Witness found no cell keys absent from Mission Control; final witness count matched its map |
| Progression preserved | Legitimate resource processing and physical delivery continued after the checkpoint |

Robot selection, identity/status/inventory details, camera focus, following and
independent layer toggles were exercised in the browser. Synthetic test maps were
never loaded into the live observer.

## Structured interface acceptance

Ten automated tests passed, covering map encodings, unknown-space preservation,
atomic rotation, read-only HTTP/WebSocket enforcement, source failures, reconnect,
event semantics, bounded cursors, persistence, restart generation changes,
corrupted-cache preservation, file export and the disabled command boundary.
The 100,000-cell synthetic diff test completed in under 0.4 seconds on this host.
That is a server diff benchmark, not a browser frame-rate claim.

The live API and atomic file export agreed on 9,033 known cells and ten robots.
A valid draft submission returned `COMMAND_CHANNEL_DISABLED`, with both submission
and execution false; the Minecraft job inbox was unchanged.

An audit through the existing scheduler produced observable job, movement and
storage events, then returned the robot. A bridge restart preserved recent event
history and rejected its old cursor with `409 RESYNC_REQUIRED`. The unchanged
browser reconnected successfully.

Three further existing scheduler jobs collected furnace output, performed a physical
robot-to-robot handoff and delivered eight iron ingots to a chest. All completed,
and actual storage inventory confirmed the result. These operations required no
Minecraft screenshots, keyboard or mouse input. They validate observation and
compatibility with existing execution, not the new strategic command interface.

## Limitations

- The new command channel is disabled pending validation and durable lifecycle
  support inside Mission Control. Enqueueing is never treated as completion.
- Ordered route rendering and historical replay controls are future work.
- Radio gaps delay observations; map and robot state reflect the last received reports.
- Semantic events are derived from sampled snapshots and can miss intermediate actions.
- Missing health, recipes, destinations or quest facts remain unknown.
- End-to-end autonomous quest decomposition is not implemented.
