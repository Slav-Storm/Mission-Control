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
- [Headless control loop acceptance results](COMMAND-VERIFICATION.md)
- [Earlier observer verification](VERIFICATION.md)
- [Daily GitHub reporting](REPORTING.md)

## Documented checkpoint — 17 September 2026

The live local Three.js observer displays discovered space and all ten robot
identities, receives incremental updates and recovers automatically after disconnects.
The same bridge exposes structured state, bounded events and atomic local snapshots.
The viewer is read-only. A separate local CLI now submits bounded SURVEY_AREA
objectives. Mission Control validates them, uses the existing scheduler, persists
their lifecycle and verifies return/completion evidence. Production and quest-level
planners remain future work. A real survey added 40 known cells and returned safely;
rejection, duplicate retry and controller/bridge restart checks passed.

Verified milestones include physical chest storage, robot crafting, a working
furnace, two tin ingots and eight iron ingots delivered to storage. The Iron Supply
objective and renewable supplies remain in progress. These are checkpoint facts,
not a live inventory feed; see the daily reports for subsequent recorded updates.

## Progress reports

Files named `day-NNNNN.md` describe completed Minecraft days. Recording started
partway through day 4; earlier daily history is not invented. An in-game recorder
detects actual day changes, and a separate local automation checks every five
minutes for reports to upload. GitHub is never the live telemetry transport.
