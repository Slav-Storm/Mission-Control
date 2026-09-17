# Quest staging acceptance checkpoint

Verified in the existing Monifactory challenge on 17 September 2026, Minecraft day 16.

## Live physical chain

1. Read the installed Iron Supply definition: 24 iron ingots, with the original quest/task IDs and introductory prerequisite preserved.
2. Submitted a validated STAGE_RESOURCE objective. A courier inspected the existing earned chest: 8 iron ingots physically present, 8 reserved, 16 missing. The operation completed; the quest remained PREPARING.
3. Submitted ACQUIRE_RESOURCE to an existing explorer at the previously observed planted grove. It harvested and returned with 32 spruce logs. Mission Control verified returned inventory, not dispatch alone. The expedition added 96 legitimately observed cells.
4. Submitted PRODUCE_ITEM for the missing 16 iron ingots. The robot supplied 11 earned logs to the existing furnace, waited for actual output, collected 16 ingots through the output side and returned. Mission Control verified its final physical inventory and job-attributed furnace report.
5. Submitted STAGE_RESOURCE again. The robot physically delivered the 16 ingots to the existing chest. A fresh peripheral inspection verified 24 total; Mission Control reserved all 24 and recorded READY FOR SUBMISSION.

No quest GUI, manual checkmark, reward selection, quest-save edit or completion command was used. FTB quest completion and claim state remain unknown; readiness describes verified physical preparation only.

## Reliability and boundaries

- Existing fleet IDs, all prior job IDs, all prior known map keys and previously recorded progression facts remain present.
- Controller and bridge restarts preserved reservations and completed command records. Duplicate immutable command submission did not create a new physical job.
- The viewer continued rendering the existing map, ten robots and the production job, and reconnected automatically after bridge restarts.
- Installed quest/configuration sources matched their extraction hashes after development; no dependency cycles or unresolved dependency IDs were found.
- Automated checks cover exact installed counts and IDs, graph traversal, unknown completion/claim states, partial stock, reservation conflicts, fresh job-attributed evidence, stock contradictions, fuel and route rejection, actual acquisition output, furnace timeout, and readiness expiry. Existing command, navigation and observer regression checks also passed.

## Current limits

The in-game preparation manifest enables Iron Supply for this first demonstration; the complete 911-quest catalog remains queryable locally. Reservations conservatively hold inventory-changing legacy jobs. There is no general reservation-release or recovery command yet; no automatic quest submission is provided. The next stage should expand validated logistics and recipes while retaining physical evidence requirements.

READY FOR SUBMISSION expires to STAGED after five minutes without re-verification. The items stay reserved. A new staging inspection refreshes readiness without consuming or claiming anything.
