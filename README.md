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
PLAN_QUEST and PREPARE_QUEST were exercised for Movin' Around and returned truthful
unsupported-recipe blockers. Automatic quest execution orchestration remains
limited; see [PRODUCTION.md](PRODUCTION.md) and
[PRODUCTION-VERIFICATION.md](PRODUCTION-VERIFICATION.md) for scope and evidence.

These are checkpoint facts, not a live inventory feed. Detailed telemetry remains
local; readiness requires fresh physical verification and expires to STAGED after
five minutes without another inspection.

## Progress reports

Files named `day-NNNNN.md` describe completed Minecraft days. Recording started
partway through day 4; earlier daily history is not invented. An in-game recorder
detects actual day changes, and a separate local automation checks every five
minutes for reports to upload. GitHub is never the live telemetry transport.
