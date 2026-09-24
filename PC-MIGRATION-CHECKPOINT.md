# PC Mission Control — migration checkpoint

24 September 2026. **The PC does not yet control the colony.** Physical dispatch remains disabled; no quest has been submitted or claimed.

Implemented locally:

- Per-run SQLite shadow ledger, transactional reservations, event deduplication, inventory revisions, request dependencies and restart checks.
- Seven deterministic ministry handlers and persistent policies. Their supported planning/allocation contracts pass isolated tests; physical execution integration remains incomplete.
- Existing map/history imported with stale inventory explicitly marked. Existing Three.js live/replay observer retained, with a read-only ministry panel.
- Disposable static export of 70,359 effective recipes, including explicit unsupported coverage. This is not yet a verified development-equivalent executable catalog.
- Bounded Codex inbox, manual handoff and usage-policy tests. No actual model invocation or ten-minute scheduled task yet.
- Lua/Node authenticated file transport: durable journal, exact-byte HMAC, SQLite commit, signed contiguous ACK and source pruning only after acknowledgment. Duplicate delivery, lost ACK and restarts pass isolated tests. A sequencing failure was preserved and corrected with ordered bounded batches.

## Fresh development audit

The original world was opened and the stationary player anchor verified. All ten turtles produced fresh local heartbeats. Read-only adjacent inventory probes independently confirmed **24 iron ingots and the wooden hook remain physically staged**. The probes left robot positions, fuel and cargo unchanged. Neither quest was submitted or claimed.

The old controller was powered off. A verified adjacent power-on exposed its existing persistence problem: **Out of space while writing the global colony snapshot**. The committed state is intact; unfinished-save evidence and the fresh failure are preserved. No world reset, restoration, quota increase or resource spawning was used.

The observer and PC shadow service remain available, but the legacy controller's source/day records are stale. Routine production and daily reporting cannot advance normally until this persistence/gateway migration is resolved. Other known storage still requires fresh inspection.

## Verification and remaining work

Twenty-one Python/Lua regression suites and twenty-two viewer tests passed. Fifteen PC tests passed. Three fresh-process Lua/Node/SQLite transport runs passed after fixing the sequencing bug. A million-cell SQLite benchmark is recorded separately; none of these claims substitutes for physical migration acceptance.

Next: bounded observation-only gateway, source enrollment and reconciliation, development catalog equivalence, approved prospecting deployment, drained epoch-fenced authority transfer, physical ministry demonstrations and the scheduled Codex checker.

Source, databases, tokens, exact coordinates, world backups and detailed telemetry remain local. Precise recovery receipts and requirement checkpoints prevent repeated physical actions. No clean world has been started. This is an implementation checkpoint, not a completion claim.
