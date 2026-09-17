# Headless Mission Control interface — v1 foundation

This extends the running observer. There is one bridge, one decoded model, and
two consumers: the browser and an external reasoning agent. Minecraft computer 0
remains authoritative. The interface performs no task scheduling, world discovery,
recipe inference, Minecraft writes, or graphical input.

This document describes the local implementation. The public repository currently
contains documentation and reports, not the executable files referenced below.

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
The CLI communicates only with 127.0.0.1:4318. `snapshot` returns the complete
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

## Command boundary: designed, deliberately not activated

`command-contract.mjs` defines versioned UUID command envelopes and the strategic
hierarchy. The first planned operation is level 2 SURVEY_AREA. LOCATE_RESOURCE and
PRODUCE_ITEM are level 3, COMPLETE_OBJECTIVE level 4. Their future planners belong
inside Mission Control. Routine commands will not be sequences of turtle keystrokes.

```powershell
node viewer/agent.mjs draft 1
node viewer/agent.mjs submit draft.json
```

The first prints a **DRAFT_ONLY** envelope. Saving it is not submission. The second
currently returns a structured REJECTED result, `COMMAND_CHANNEL_DISABLED`, with
`submittedToMissionControl:false` and `executed:false` (exit code 2). Invalid
envelopes receive `INVALID_COMMAND`. Nothing is written to Minecraft. This is a
fail-closed transport boundary, not a claim that Mission Control has rejected or
executed an objective. There is no active command inbox, no POST route and no
browser-accessible control endpoint. All WebSocket client messages remain rejected.

## Next implementation checkpoint: validation must live inside Mission Control

The existing developer `scripts/dispatch.py` is a legacy job-queue tool, not the
future strategic command interface. Wrapping it with an HTTP POST would bypass
the requirements below, so this checkpoint does not do that.

Implement a small `software/lib/objectives.lua` first, tested offline, beginning
with SURVEY_AREA. Then integrate it into control.lua at an idle, checkpointed
boundary. Turtles keep physical safety checks; the bridge never claims acceptance.

Required transaction and lifecycle:

1. A separate trusted local agent transport durably queues an immutable envelope
   with schema version, UUID, operation, parameters, creation/expiry time and
   optional expected-state preconditions. Record SUBMITTED as a transport receipt.
2. Mission Control deduplicates by UUID and a canonical request digest. Same UUID
   and same payload returns the original receipt/result; different payload is an
   explicit ID_REUSE_CONFLICT and must never overwrite or rerun the original.
3. Mission Control validates bootstrap sealed, operation allowlist, fresh radio,
   actual robot capabilities/status, no ambiguous navigation, required resources,
   safe known navigation and return fuel, and existing task ownership. Reject with
   structured reasons such as INSUFFICIENT_RETURN_FUEL, ROBOT_BUSY, STALE_TELEMETRY,
   UNKNOWN_ROUTE, MISSING_INPUTS, UNSUPPORTED_OPERATION or EXPIRED_COMMAND.
4. Atomically persist ACCEPTED plus job reservations, deterministic child job IDs
   and the plan **before** dispatch. Recheck safety/ownership at dispatch. Expiry
   before acceptance/start does not silently cancel a robot already underground.
5. Report RUNNING only from actual executor acknowledgement. Each job carries its
   parent command ID, and progress is reported, not guessed from enqueue time.
6. Report COMPLETED only after the operation's completion predicate is verified.
   A returned survey is different from finding the requested ore; a crafting call
   is different from delivered inventory; a crafted quest item is different from
   recorded quest completion. Persist the evidence and resulting inventories.
7. Failed or rejected commands remain queryable. Failed partial production must
   preserve the physical materials, completed subtasks, failure reason and recovery
   position; retries must never replay already-completed physical actions blindly.
8. After restart, reconcile durable records with robot outcomes. Ambiguous in-flight
   actions require recovery, never optimistic completion or automatic replay.

Transport should be a separate local IPC/CLI capability with an atomic per-command
file spool and acknowledged results, or an equivalently protected agent endpoint.
Do not expose it through the viewer origin, JavaScript bundle, public bind address,
or shared WebSocket. A loopback-only POST by itself is not a sufficient browser
separation. The command service must also preserve existing manual job ownership
until the legacy dispatcher is retired.

Required acceptance tests before enabling writes: duplicate retries and conflicting
IDs, stale/fuel/resource rejections, two objectives contending for one robot,
crashes before/after acceptance and dispatch, worker failure, durable terminal
results, actual bounded survey with return, and no viewer command access. These
changes are intentionally deferred; the live viewer and external reads work now.

Later checkpoints add Mission Control recipe/inventory planning, physical delivery
verification, renewable fuel management, and quest integration. Until then graphical
control is only needed for mechanics the colony cannot yet expose; ordinary state
inspection already requires no graphical control. The player remains immobile.
