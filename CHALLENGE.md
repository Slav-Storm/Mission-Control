# Challenge rules

The player remains at the recorded starting position for the entire challenge.
Camera movement is permitted; walking, jumping, swimming, flying, riding and
teleporting to relocate are forbidden. Accidental displacement must be documented
and corrected to the original anchor. The exact anchor is retained locally.

## Bootstrap and resources

The user authorised a starting fleet of ten specialised turtles and enough fuel
to operate them. The recorded bootstrap includes one advanced Mission Control
computer, ten turtles, eleven wireless modems, ten diamond pickaxes and 640 coal.
The coal supplied 5,120 fuel units per turtle. Bootstrap is permanently sealed:
future resources, tools, machines, upgrades and replacements must come from gameplay.

Physical storage and crafting infrastructure were subsequently obtained through
the colony. Items travel in robot inventories, chests and legitimate transport
systems; the player's inventory is not global storage.

## Knowledge and autonomy

Mission Control knows what robots actually report. Unknown terrain stays unknown.
No seed analysis, region-file inspection, external maps or commands reveal resources.
Monifactory's ore distribution and processing recipes guide prospecting; ordinary
Minecraft ore assumptions are not treated as authoritative.

Roles are assignments rather than permanent robot identities. Exploration, mining,
surveying, forestry, transport, construction and maintenance can evolve into a shared
task system. Persistent records preserve identities, jobs, poses, fuel, observations,
storage, discoveries, failures and outcomes across restarts.

Failures are part of the run. Do not reload to erase robot losses or failed jobs.
Attempt legitimate recovery, preserve the evidence and improve the software.
Manufacture replacements legitimately if recovery fails.

## System responsibilities

| Component | Responsibility |
| --- | --- |
| Turtles | Physically interact with Minecraft and apply local safety checks |
| Mission Control | Own knowledge, scheduling, execution and outcome verification |
| Local bridge | Expose projections of authoritative state to local consumers |
| 3D viewer | Read-only human observation |
| Codex | Reason about structured state and, eventually, submit strategic objectives |
| GitHub | Store documentation and concise historical reports |

The long-term target is objective-driven exploration, logistics, industry and quest
progression without routine graphical input. Current capabilities and deferred work
are documented separately; an accepted design is not evidence of execution.
