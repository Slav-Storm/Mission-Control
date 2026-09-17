# Run isolation and Minecraft-day replay

Mission Control remains authoritative for the current colony. Portable software
and static Monifactory knowledge are separated from physical run state. The
existing development colony was checkpointed and adopted into a persistent UUID
namespace. No new Minecraft world was started, restored or substituted.

## Knowledge and state

`software/` and `knowledge/` contain programs, safety rules, command schemas, the
911-quest catalog and graph, recipes and execution implementations. Capability
definitions describe implementation knowledge, never physical availability.
Static quest manifests no longer carry development-world completion observations.

ComputerCraft state uses an `mc-run-state/1` envelope with `runId` and `payload`.
Every computer has a run manifest. The colony, radio messages and protocol, new
commands, exports and archives are run-scoped. The host registry binds a run to
one explicit source directory. Mismatched or unscoped operational state fails
closed before map decoding. Commands are never silently retagged. The bridge
invalidates current state if source identity changes.

Terrain, clear cells, hazards, resources, poses, inventories, routes, machines,
jobs, commands, reservations, production, staging, quest observations and the
player anchor belong exclusively to their run. Iron Supply's 24 reserved ingots
belong only to the development run.

## Future clean initialization

`python scripts/init_run.py --output NEW_DIRECTORY --name NAME` creates a unique
**offline, unactivated** package. It refuses existing destinations and Minecraft
save/computer directories. It copies portable software and knowledge, creates
empty physical state and history index, and leaves bootstrap unsealed. It does
not select, create or deploy a Minecraft world.

Future activation requires a new registered source, legitimately observed anchor
and robot poses, and independently verified infrastructure. Start recording before
dispatch. The first real day sample determines the timeline; no day 0 evidence is
invented. Never copy development computer state or its manifest into a clean run.
The guard detects namespace mismatches; it is not a hidden world fingerprint or
protection against deliberately cloning both state and its identity together.

## Local archive

`runs/RUN_ID/` contains separate `history`, `interface`, `computer-journals`,
`terminal-records` and `reports` directories. Interface exports are replaceable
projections. Historical records never feed back into current robot planning.
Detailed telemetry stays local and operates without GitHub.

The bridge writes compressed checkpoints at day boundaries, restart and a
15-minute interval. Between checkpoints it batches compressed map/entity deltas
every five seconds. Atomic indexes identify committed journal byte prefixes.
Torn uncommitted tails are excluded; failed index commits can be retried without
duplicate changes. Old checkpoint files remain available.

Legacy development journals were explicitly attributed to the checkpointed run.
SHA-256-verified compressed copies preserve approximately 927 MB in 110 MB; raw
originals are retained too. They are evidence, not a second current database.

## ComputerCraft retention

A separate trusted local collector flushes and verifies archives before issuing
run-scoped acknowledgements. Mission Control checks unchanged local bytes/records
before pruning. The browser cannot acknowledge archives or command robots.

Current maps, navigation recovery, active work, command recovery, reservations
and staging references are protected. The latest 64 eligible terminal jobs and
12 terminal commands remain in full, plus pinned records. Older records retain
IDs, outcomes, reconciliation evidence and archive hashes. Canonical command
requests remain for idempotence. Full detail stays retrievable from the archive.

Journals rotate at 32 KB. Beyond a 96 KB closed-journal backlog, non-authoritative
journaling pauses with a bounded gap notice; existing bytes and robot execution
are preserved. Closed daily reports can be archived locally before GitHub upload.
The publisher reads these same run-tagged reports, independently of telemetry.

This bounds bulky history, not all possible growth. Current maps, compact command
receipts and pinned evidence still consume ComputerCraft space. No quota was
raised. The large-map archive benchmark does not imply unlimited operational
map capacity inside ComputerCraft.

## Existing viewer timeline

The Three.js observer now has a day slider, previous/next, Play/Pause,
1x/2x/5x/10x playback and LIVE. Historical mode is clearly labeled. Incoming live
telemetry updates a separate cache while the displayed historical state remains
fixed. LIVE returns immediately to the newest received authoritative snapshot.
Reconnection obtains a fresh snapshot as before.

Development map history begins on **Minecraft day 10**. Earlier daily summaries
are context only. A selected day shows its latest reconstructable sample; partial
days are labeled. Unknown terrain remains absent. Source/robot times, controller
receipt times, observer times and day samples retain separate meanings. Baselines
mean “known by this sample,” not an exact discovery time. Outages can leave gaps.

Milestones derive from recorded production, capability, fleet and preparation
evidence, including Iron Supply readiness transitions. They do not assert quest
submission or claiming. Moving backward removes later discoveries; moving forward
restores them. Neither action changes Minecraft.

## Headless access

The existing localhost API adds these read-only routes:

```text
GET /api/v1/runs
GET /api/v1/history/RUN_ID/days
GET /api/v1/history/RUN_ID/day/N
GET /api/v1/history/RUN_ID/records/jobs/JOB_ID
GET /api/v1/history/RUN_ID/records/commands/COMMAND_ID
```

Archived records explicitly declare themselves historical, not current authority.
GET/HEAD-only HTTP and receive-only WebSockets are unchanged. Multiple registered
runs are supported by storage/API; polished run-selection UI remains future work.

```powershell
node viewer/agent.mjs runs
node viewer/agent.mjs history RUN_ID
node viewer/agent.mjs history RUN_ID 10
node viewer/agent.mjs archived-record jobs JOB_ID
python scripts/archive_cc.py --watch
```

New objective drafts automatically use the active run. Planning and execution
remain in Mission Control. See [HARDENING-VERIFICATION.md](HARDENING-VERIFICATION.md).
