# Local 3D observer and telemetry architecture

This document describes the existing local implementation. Commands and source paths
below refer to that installation; this public repository is documentation-only.

Open **http://127.0.0.1:4318/**. Start with `powershell -File viewer/start.ps1`
from the project root. The script uses the installed bundled Node runtime and
starts a hidden process. Dependencies are pinned in package-lock.json; reinstall
with `npm ci --ignore-scripts` in viewer if needed. No CDN or external telemetry
service is used. To stop, use the PID in `viewer/runtime/server.json`, after
checking that it is still the observer Node process. Stopping it cannot stop robots.

The same bridge now provides a versioned headless API, CLI, atomic file snapshot
and bounded semantic event feed. See [HEADLESS.md](HEADLESS.md) for commands,
cursor/reconnection rules and the future command validation boundary. The viewer
remains read-only; command submission is deliberately disabled until Mission
Control implements durable validation, acknowledgement and completion evidence.

## Authority and architecture

Robots → CC:Tweaked rednet → computer 0 `control.lua` → existing JSON snapshots
→ read-only Node bridge (one-second polling) → WebSocket → Three.js.

The bridge opens only these two existing Mission Control files:

* `computercraft/computer/0/data/colony.json`: authoritative received observations,
  robots, jobs, storage, production and objectives.
* `computercraft/computer/0/data/current-day.json`: actual Minecraft day/hour,
  recorded player anchor, quest context and capture time (five-second samples).

It does not read region files, seed data, level.dat, private robot maps, commands,
inboxes, or robot navigation files. It never writes to the Minecraft instance.
This is a decoded presentation of the existing map, not an independent mapper.
No Mission Control or worker software changes were needed for the viewer.

### Existing telemetry schema

* Map encoding 2 stores `discoveries.cells["x,y,z"]` as a 1-based index into
  `discoveries.palette`, where entries are `[blockName, blockState, oreBoolean]`.
  Index 0 means inspected empty/clear space. Unknown keys remain absent.
  Legacy encoding 1 and the original verbose format are also supported.
* Cells are individual absolute Minecraft block coordinates, not regions.
  Coordinates are never sourced from terrain files. Ore flags come from actual
  robot block inspection tags; resource colors do not infer veins beyond samples.
* `robots[id].pose` stores x/y/z and heading: 0 north (-Z), 1 east (+X),
  2 south (+Z), 3 west (-X). Positions are last **received by Mission Control**,
  not extrapolated. Normal radio has limited range. Reports older than 15 seconds
  are marked stale, including while Minecraft is paused.
* Each robot record contains label, role, status, fuel, optional current job,
  inventory, reason/activity, robot time, Mission Control `received`, and outcomes.
  Fuel is moves remaining; no invented percentage or maximum is displayed.
* Jobs store request and status. Explicit goals may be displayed as destinations.
  `knownCells` is an unordered traversable corridor, **not a route polyline**.
  Ordered breadcrumbs exist on some robots but are not centrally reported;
  route rendering remains future work. Received position samples are shown as
  disconnected dots, avoiding invented paths across radio gaps.
* Storage records contain block name, location, actual peripheral inventory and
  timestamp. Production and objectives remain intact in the authoritative model.
* Robot telemetry changes every ~5 seconds when idle and more frequently during
  action. Mission Control batches persistence at one second. Radio gaps can delay
  entire map batches until a robot returns. The viewer cannot show discoveries
  Mission Control has not received.
* Individual current map cells have no observation timestamp. Existing event
  logs, per-robot history and daily archives are preserved, not rewritten.

### Isolation, transport and history

HTTP and WebSocket bind only to **127.0.0.1:4318**. A fixed static-file allowlist,
Host/Origin checks, GET/HEAD-only HTTP and a receive-only WebSocket prevent control
requests. Any client application message closes that WebSocket. Slow clients
are disconnected and resynchronize; they cannot backpressure Minecraft.

Atomic JSON rotation can briefly remove the current file. Reads retry with short
backoff and release file handles immediately. Malformed/unavailable input retains
the last good snapshot with an explicit source-unavailable state. `.bak` is never
misrepresented as a fresh snapshot. The independently sampled day and colony
files may differ by a few seconds; their timestamps are preserved.

Each connection receives a fresh full snapshot, session UUID and revision, then
cell upserts/removals and metadata. Missing revisions trigger reconnection.
The viewer batches geometry rebuilding by 16×16×16 chunks, using InstancedMesh
for blocks and point buffers for inspected clear space. New cells briefly glow.
Height clipping and layer toggles affect only rendering. All ten robot markers
have identity and heading; select from the fleet or map, focus or follow.

`viewer/runtime/history/` holds **local-only** append-only session journals:
initial snapshot followed by deltas, original robot timestamps and observer
receipt times. These distinguish observation receipt from the unknown original
cell discovery time. They support future replay; replay UI is not implemented.
In-memory position trails retain the latest 2,000 samples per robot; full recorded
session history remains on disk. History write failure is isolated from reading
and rendering. Monitor disk use for long unattended sessions.

The Mission Control marker uses its documented bootstrap position. No terrain
is filled around it. Machine geometry is shown only where block observations or
reported storage locations support it. Advanced factory and ordered route layers
await suitable authoritative telemetry.

GitHub day-summary publishing remains separate; see [Daily reporting](REPORTING.md). This server has no GitHub integration, upload code, or outbound client.

## Checkpoint

A local pre-observer checkpoint contains an opaque world-file archive,
project archive and SHA-256 manifest, taken with the integrated server paused.
No world reset, reload or restore was performed. This is a disk checkpoint, not
a process-memory snapshot; running Lua stacks are not captured. Recovery guards
remain necessary if a future restart interrupts a physical robot action.

## Validation

`npm test` from the local `viewer` directory runs both observer and interface tests.
The observer suite checks all map encodings, unknown-space
preservation, atomic rotation, read-only behavior, disconnect/reconnect, origin
checks, source failures, deltas and a 100,000-cell synthetic map. Synthetic data
is confined to tests and is never injected into the live map.

Three.js references: [InstancedMesh](https://threejs.org/docs/#InstancedMesh),
[OrbitControls](https://threejs.org/docs/#OrbitControls). Versions are pinned and
all browser assets are served locally.

See [verification results](VERIFICATION.md) for live acceptance evidence and
[the headless interface](HEADLESS.md) for structured state and event access.
