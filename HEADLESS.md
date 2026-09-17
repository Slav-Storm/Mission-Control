# Headless Mission Control interface — v1 foundation

This extends the running observer. There is one bridge, one decoded model, and
two consumers: the browser and an external reasoning agent. Minecraft computer 0
remains authoritative. The bridge performs no task scheduling, world discovery or recipe inference.
The CLI can now submit immutable objective requests; validation and scheduling remain
inside Mission Control. No graphical input is required.

This describes the local implementation; this public repository contains documentation
and reports, not the executable files referenced below.

## Available now

From the project root, with Node on PATH:

```powershell
node viewer/agent.mjs status
node viewer/agent.mjs robot 6
node viewer/agent.mjs jobs --status failed
node viewer/agent.mjs resources
node viewer/agent.mjs infrastructure
node viewer/agent.mjs progression
node viewer/agent.mjs production
node viewer/agent.mjs events --limit 20
node viewer/agent.mjs capabilities
```

Commands produce JSON and require no screenshots, mouse, keyboard or internet.
Read commands communicate only with 127.0.0.1:4318. Objective submission uses
the separate local file transport described in CONTROL.md. `snapshot` returns the complete
model; `world` returns its known cells. `fleet` includes identities, roles, poses,
headings, reported fuel, slot inventories, capabilities, current jobs, outcomes,
timestamps and any reported activity. Job records preserve available reason and
progress fields rather than inventing them. Missing robot health, machine recipes
and ordered routes remain unknown.

HTTP GET/HEAD endpoints:

| Endpoint | Meaning |
| --- | --- |
| `/api/v1/snapshot` | Same model as existing `/snapshot`; schema version and event cursor added |
| `/api/v1/status` | Snapshot metadata without world cells/trails, for lightweight routine reads |
| `/api/v1/state/fleet` | Existing robot records |
| `/api/v1/state/jobs?status=failed` | Job records; optional exact status filter |
| `/api/v1/state/world` | Existing decoded cells, including observed clear space |
| `/api/v1/state/resources` | Ore/hazard indexes referencing those same cell keys |
| `/api/v1/state/infrastructure` | Reported storage inventories, observed blocks, documented control location |
| `/api/v1/state/progression` | Recorded day, objectives and known quest context |
| `/api/v1/state/production` | Reported outputs, recipe IDs and robot operation capabilities |
| `/api/v1/state/commands?status=COMPLETED` | Durable command records; optional exact status or `active` filter |
| `/api/v1/state/routes` | Centrally reported routes if present; otherwise explicitly unavailable |
| `/api/v1/events` | Bounded recent events and pagination cursor |
| `/api/v1/capabilities` | Version, supported reads, limits and disabled command gate |

All views are projections of the same in-memory model. There is no second mapper
or authoritative resource database. Indexes identify observed blocks, not inferred
vein boundaries. A production record is evidence of that reported production;
it does not prove the next requested recipe can run. Quest facts come from the
existing recorder, not a newly installed quest integration.

## Snapshot and event cursor protocol

1. Read `/api/v1/snapshot`; retain `eventCursor.streamId` and `sequence`.
2. Read `/api/v1/events?after=SEQUENCE&streamId=UUID&limit=100`.
3. Process results in sequence order; advance to `nextAfter`. Repeat while
   `hasMore` is true. Maximum page size is 200; recent retention is 1,000 events.
4. HTTP 409 `RESYNC_REQUIRED` means the cursor is older than retention, from a
   different process generation, or ahead of available data. Read a fresh snapshot.
5. Check `sourceOK`, source timestamps, robot `received` ages and
   `interfacePersistenceError`. A fresh HTTP response alone does not prove fresh
   Minecraft telemetry. Minecraft pauses and radio outages remain visible.

The existing receive-only `/live` WebSocket remains compatible with the viewer.
Its map deltas now also include semantic events and a cursor. Its revision numbers
are per-process. Missing revisions require a fresh connection/snapshot as before.
The bounded event endpoint supports agents that prefer polling rather than sockets.
Semantic events notify an agent to consult current views; they are **not** a full
replacement for map deltas and cannot alone reconstruct every changed field.

Event types include BRIDGE_RESYNC, ROBOT_POSITION_UPDATED, ROBOT_STATUS_CHANGED,
ROBOT_ACTIVITY_REPORTED, JOB_QUEUED/STARTED/COMPLETED/FAILED/BLOCKED/CANCELLED,
RESOURCE_DISCOVERED, RESOURCE_OBSERVATION_CHANGED, HAZARD_OBSERVED, WORLD_UPDATED,
STORAGE_UPDATED, PRODUCTION_REPORTED, OBJECTIVE_COMPLETED,
OBJECTIVE_STATUS_CHANGED, QUEST_COMPLETION_RECORDED, FLEET_EXPANDED and
MINECRAFT_DAY_CHANGED. Only transitions actually supported by telemetry are emitted.
There are no fabricated ROBOT_LOST, RESOURCE_DEPLETED or FACTORY_CREATED claims.

Every event has a unique generation/sequence ID, observer UTC timestamp, snapshot
revision, Minecraft day and its sample timestamp, plus original source time when
available. The day is the last recorded sample, not an exact inferred event tick.
Current cell data lacks discovery timestamps; the bridge labels receipt times.
Intermediate actions between samples can be missed. A first connection or restart
emits BRIDGE_RESYNC rather than pretending the existing colony was just discovered.

## File access and persistence

Everything below stays in this workspace, excluded from GitHub:

```text
viewer/runtime/interface/
  state/snapshot.json             complete derived model; refreshed up to every 5s
  events/recent.json              atomic bounded event checkpoint + sequence
  events/recent.jsonl             atomic JSONL convenience view, refreshed up to every 5s
  events/YYYY-MM-DD-STREAM.jsonl  append-only session event archive
```

Snapshots and recent files are independently written through unique temporary
files and atomic rename with bounded Windows sharing retries. Each snapshot
includes its event cursor. There is no implied transaction across multiple files:
after a snapshot, follow its cursor via the API, or retry the newer recent file.
An older JSONL cache must not be interpreted as proof that no newer events exist.
Files remain readable with the server stopped, but must be treated as stale based
on their timestamps. Consumers never edit these caches to change Minecraft.

Recent history is restored on restart. The stream generation always changes so
an interrupted write cannot cause old cursors or IDs to be reused ambiguously.
Old records retain their original IDs. An invalid recent checkpoint is preserved
with an `.unreadable-UUID` suffix and recovery uses a new generation. Full event
archives and the pre-existing raw snapshot/delta journals remain local. A crash
can truncate an archive's final line; ignore incomplete final lines. These are
observer histories, not a lossless in-game event bus.

## Validated command interface

The separate local CLI file transport is now enabled for SURVEY_AREA and the bounded quest-staging resource operations. Mission
Control validates requests, reserves an existing robot job and records durable
lifecycle and completion evidence. The browser and bridge remain read-only.
See [CONTROL.md](CONTROL.md) for submission, querying, validation, idempotence,
restart behaviour and current recovery limits. See [QUESTS.md](QUESTS.md) for installed quest queries, inventory planning and
physical reservation semantics. More general strategic operations remain planned. No HTTP POST or browser command channel has been introduced.
