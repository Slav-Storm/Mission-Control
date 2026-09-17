# Quest intelligence and physical staging

Mission Control reads static definitions from the installed Monifactory pack. The catalog preserves 911 quest IDs in 15 chapters and 1,205 dependency links, with no unresolved dependency IDs. It includes original task/reward definitions, English descriptions, source hashes, and dependency rules. No Minecraft terrain or quest save files are used to construct it.

The installed task types are item, checkmark, statistic, gamestage, dimension, custom and observation. Filters, NBT matching and custom requirements remain explicit unknowns where the current preparation model cannot evaluate them. Item counts follow the installed FTB Quests implementation: the task count is authoritative, not the display stack count.

## Headless queries

The existing local API provides `/api/v1/quests`, `/api/v1/quests?filter=available`, `/api/v1/quests?filter=ready` and `/api/v1/quests/ID`. Append `/requirements`, `/dependencies`, `/blockers` or `/staging` for focused views. The CLI equivalents are `quests [available|ready]` and `quest ID [requirements|dependencies|blockers|staging]`.

Static definitions explain what the pack requires. Mission Control's reported inventories and quest preparation records describe what the colony has verified. Neither stock in a chest nor a successful robot job proves quest-system completion or reward claiming. The three previously recorded introductory completions have historical provenance; other completion and claim states remain unknown.

## Physical staging

QUEST STAGING uses an existing legitimately crafted chest. A staging objective inspects its real inventory through a turtle inventory peripheral, deposits matching carried items if needed, then sends a job-attributed inventory report. Mission Control reserves only the quantity physically verified there. Missing stock is reported as a structured shortage.

Reservations live in the existing colony database beside jobs and commands. Initial enforcement is deliberately conservative: inventory-changing legacy jobs are held while reservations exist, and validated resource operations are serialized. Survey and inspection work remain available. A contradictory inventory report blocks preparation. External readiness requires a recent inspection; after five minutes it becomes STAGED with a re-verification blocker.

## Incremental objective support

- `STAGE_RESOURCE`: exact-item quest staging and physical reservation. A partial staging operation may complete while the quest remains PREPARING.
- `ACQUIRE_RESOURCE`: bounded spruce timber acquisition at an already observed tree or planted grove, with actual returned inventory evidence.
- `PRODUCE_ITEM`: the verified ordinary-magnetite furnace route for iron, with real fuel, known access routes, output collection and returned inventory evidence.

These use the existing durable SUBMITTED → VALIDATING → ACCEPTED → RUNNING → COMPLETED lifecycle. Invalid requests are REJECTED; failed execution retains evidence and requires recovery where appropriate. Dispatch is never completion. No arbitrary remote movement or unvalidated plan endpoint is exposed.

The complete catalog is local; only an explicitly supported exact-item manifest is installed in the in-game controller for this first preparation test. This is not a general recipe optimizer. Unsupported recipes, dependency rules, crafting-only tasks and filter matching remain visible limitations.

## Human authorization boundary

READY FOR SUBMISSION means physically prepared and reserved, with known prerequisites supported by recorded observations. It does not mean submitted, completed in FTB Quests, or claimed. No command in this stage opens the quest screen, selects rewards, checks a manual task, edits quest saves, or forces completion. Final submission and claiming require explicit human authorization.

The 3D viewer remains a read-only observer. Live telemetry stays local. GitHub receives documentation and concise historical summaries separately.
