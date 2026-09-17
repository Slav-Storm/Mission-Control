# Mission Control

An immobile-player Minecraft challenge in Monifactory expert mode. Ten specialised
programmable turtles explore, mine, craft and transport resources while their human
commander remains at Mission Control. The initial bootstrap is permanently sealed.

This repository contains project documentation and concise historical progress
reports. The runnable implementation remains local; this is not yet a source-code
release. Detailed live telemetry, coordinates, routes, world saves and logs stay local.

## Documentation

- [Challenge rules and operating principles](CHALLENGE.md)
- [Local 3D observer and telemetry architecture](ARCHITECTURE.md)
- [Headless state API and event protocol](HEADLESS.md)
- [Validated command submission and recovery semantics](CONTROL.md)
- [Quest intelligence and physical staging](QUESTS.md)
- [Production planning and quest preparation](PRODUCTION.md)
- [Production generalization acceptance results](PRODUCTION-VERIFICATION.md)
- [Reusable crafting and quest orchestration checkpoint](CAPABILITY-VERIFICATION.md)
- [Concurrent operations and fuel policy](OPERATIONS.md)
- [Operations and renewable fuel verification](OPERATIONS-VERIFICATION.md)
- [Run isolation, retention and Minecraft-day replay](RUNS-HISTORY.md)
- [Infrastructure-hardening verification](HARDENING-VERIFICATION.md)
- [Headless control loop acceptance results](COMMAND-VERIFICATION.md)
- [Earlier observer verification](VERIFICATION.md)
- [Daily GitHub reporting](REPORTING.md)

## Documented checkpoint — 17 September 2026

The live local Three.js observer displays discovered space and all ten robot
identities, receives incremental updates and recovers automatically after disconnects.
The same bridge exposes structured state, bounded events and atomic local snapshots.
The viewer is read-only. The same validated command lifecycle now supports bounded
survey, timber acquisition, furnace iron production and physical quest staging.
Installed static quest definitions expose 911 quests and their dependencies through
the headless interface. No undiscovered terrain is read from world files.

Iron Supply is physically prepared: 24 iron ingots were verified in the existing
earned chest and reserved. The test acquired 32 logs, produced the missing 16 iron
ingots, delivered them and stopped at READY FOR SUBMISSION. No quest submission,
manual checkmark or reward claim occurred.

A bounded production planner now separates recipe knowledge from verified colony
capabilities, recursively expands ingredients and respects quest reservations.
The generalized logs-to-planks-to-sticks executor physically produced four sticks
through two verified child jobs. A separate regression mined fresh magnetite and
produced one additional iron ingot without consuming the reserved 24.
The next blocker-driven stage added source-backed shaped recipes, selective
inventory access, physical ingredient delivery and bounded quest orchestration.
Movin' Around now also reached READY FOR SUBMISSION: one wooden hook is physically
staged and reserved. Iron Supply still has its separate 24 reserved ingots. Neither
quest has been submitted or claimed. See [CAPABILITY-VERIFICATION.md](CAPABILITY-VERIFICATION.md)
for the successful chain, recovery incidents and remaining limits.

These are checkpoint facts, not a live inventory feed. Detailed telemetry remains
local; readiness requires fresh physical verification and expires to STAGED after
five minutes without another inspection.

The development operations manager has now generated useful concurrent survey,
forestry and logistics jobs through the existing scheduler. Three robots were
physically active together. Grove repair verified four replanted beds, and three
automatic refuel jobs consumed twelve earned logs for 180 measured fuel. Both
quest reservations remain intact and unsubmitted. The first supervised operating
window is stopped; the observer and archive remain live. Fuel independence is not
yet established. See [OPERATIONS-VERIFICATION.md](OPERATIONS-VERIFICATION.md).

The infrastructure checkpoint added two robot-built chests and verified transfers
across multiple physical inventories. Storage now has 81 measured slots. Robot 11
remains blocked by the installed HV component chain, commissioning support and
sustainable fuel capacity; no additional robot has been manufactured. Both staged
quests remain protected. See [INFRASTRUCTURE-VERIFICATION.md](INFRASTRUCTURE-VERIFICATION.md)
for physical evidence, preserved failures, recovery and current limits.

## Progress reports

The development colony now has a persistent run identity. Portable quest and
recipe knowledge is separated from physical state, and a tested offline initializer
inherits no terrain or inventory. Local compressed history supports the existing
viewer's day replay from day 10 onward. Live operations continue independently
of historical viewing. No clean world has been started.

Files named `day-NNNNN.md` describe completed Minecraft days. Recording started
partway through day 4; earlier daily history is not invented. An in-game recorder
detects actual day changes, and a separate local automation checks every five
minutes for reports to upload. GitHub is never the live telemetry transport.
