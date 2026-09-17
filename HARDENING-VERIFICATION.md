# Infrastructure-hardening verification

The pre-migration checkpoint preserved all eleven computer directories, software,
knowledge, an observer snapshot and the legacy-history inventory. No world reset,
restore, new Minecraft run, quest submission or reward claim occurred.

## Preservation and isolation

- All ten robot identities and roles were preserved and reported fresh telemetry.
- All 199 pre-checkpoint job IDs, 19 command IDs and 9,286 map cells remain.
- Storage contents match the checkpoint. All 24 Iron Supply ingots remain reserved.
  Fresh headless staging verification again reached READY FOR SUBMISSION. Existing
  readiness freshness still expires to STAGED after five minutes without inspection.
- The 911-quest catalog and recipe knowledge remain available.
- Disposable offline test run B inherited none of synthetic run A's map, fleet,
  storage, jobs, commands, reservations, production, staging, quest observations
  or capability availability. Portable quest/recipe knowledge remained loaded.
- Wrong-run state and commands were rejected before map decoding or dispatch.
  No disposable test was deployed to Minecraft.

## Archive and replay

- About 927 MB of legacy journals were preserved in 110 MB of verified compressed
  copies. No malformed lines or revision gaps were found within those files;
  this does not prove continuous observation between recorded sessions.
- Day 10 reconstructs 8,669 cells; day 11 reconstructs 9,033; current state has
  9,286. Earlier/later browser selection removes and restores later discoveries.
- Browser checks covered selection, stepping, automatic replay, pause and LIVE.
  The existing rendered 3D map and all ten robot identities remained visible.
- A live survey completed while historical mode was displayed. Bridge restart
  and reconnection did not halt robots or change the selected historical map.
- Synthetic tests cover frozen history during live changes, latest-state LIVE
  return, archive reopening, torn tails, failed index commits, source mismatch
  invalidation and HTTP write rejection.
- Pruned terminal records were verified against SHA-256 archive references.
  Active/recovery/staging references, open logs and authoritative files are excluded.

## Performance and limits

A 100,000-cell synthetic map took approximately 432 ms to compute an archive
delta on this host. Full JSON was 4.07 MB; a gzip checkpoint was 274 KB. One cell
change plus robot telemetry produced a roughly 700-byte compressed delta. With
two checkpoints per 20-minute day and one such batch every five seconds, 100 days
would occupy about 71 MB. This is an illustrative workload calculation, not a
guarantee for arbitrary activity.

The controller used about 874 KB after verified retention, versus roughly 978 KB
during migration before compaction. Usage varies with state and journal rotation.
No ComputerCraft quota increase was used. Compact reconciliation receipts and
current maps still grow and need future capacity planning.

## Regression scope

All 18 JavaScript observer/interface/history tests and all twelve Python/Lua suites
passed. Coverage includes scheduler and validated lifecycle, survey, acquisition,
furnace and recursive crafting production, physical staging, reservations,
production/quest planning, PREPARE_QUEST blockers, navigation safety, persistence
interruptions and archive retention.

Live checks in this stage exercised SURVEY_AREA, PLAN_PRODUCTION, PLAN_QUEST,
PREPARE_QUEST's truthful blocker result and STAGE_RESOURCE reinspection. Acquisition
and production retain their prior physical acceptance evidence and passed automated
regression here; no unnecessary production consumed staged iron. Daily export
remains separate and consumes run-tagged closed reports.

History is sampled colony knowledge, not a lossless recording of Minecraft. It
starts on day 10 for this world. The clean-run initializer is offline only.
See [RUNS-HISTORY.md](RUNS-HISTORY.md) for architecture and operational boundaries.
