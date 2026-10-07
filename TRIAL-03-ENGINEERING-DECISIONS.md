# Trial 03 engineering decisions

7 October 2026. This is a sanitized summary of the durable local decision journal. Native evidence, source, databases, world coordinates, host paths and credentials remain local. Decisions describe implemented behavior and its limits; isolated fixtures are not autonomous-world progress.

## T03-ADR-001 — Preserve old runtimes; witness basic extraction separately

**Context:** clean colonies had no chest, while acquisition assumed shared storage. The existing mining executor also admitted ores rather than ordinary starting materials.

**Choice:** extend the existing physical block/cargo path with a narrow basic-material whitelist and a separately hashed portable runtime. Mining still needs a legitimate observed source. Native inspection before extraction and actual inventory changes provide completion evidence. Logistics can reserve the output in the collecting turtle's real container.

**Rejected:** fictitious shared storage, inventory rows written from intended output, copying development capability availability, or replacing the accepted historical runtime.

**Verified:** a disposable Creative fixture recovered ordinary materials; an independently commissioned disposable fixture with prepared test terrain subsequently let its Director acquire six cobblestone through six physical jobs without shared storage. Cargo and reservations were observed, commands retired, and claims released. These fixture resources never entered Trial 03.

**Limit:** a witnessed executor does not conjure a source, infrastructure or crafting tool in a fresh world. Restoring old PC software must never roll back physical effects.

## T03-ADR-002 — Compare recipes, not just export identifiers

**Context:** normal startup changes the exporter generation. Some installed exports also differ in real recipe values; this is not merely a random identifier problem.

**Choice:** exact recipe-record equivalence can tolerate generation/timestamp-only changes. Genuine changes remain blocked for production. After an already committed fresh authority, a separately verified non-recipe comparison may permit the existing non-recipe operations while excluding production. Named registries, tag membership, runtime and authority must still match. A new epoch-zero run cannot use this path to skip initial binding.

**Rejected:** trusting any new generation, ignoring changed processing costs, approving every recipe, or treating a successful inspection as production approval.

**Verified:** equivalence/mismatch unit tests and a real isolated Minecraft restart. The latter retained old terminal jobs and admitted only new non-recipe work; production was absent from its permit. Normal startup can therefore recover supported physical observation work without accepting altered recipes.

**Limit:** actual changed recipes still need affected execution capabilities reverified. This is not blanket recipe equivalence.

## T03-ADR-003 — Keep the first-workbench boundary honest

**Context:** the unchanged starting turtles have a diamond pickaxe and wireless modem. The installed native Lua API has no crafting function without a workbench upgrade. Monifactory's first table recipe requires two flint and two logs, but knowing that recipe does not grant execution.

**Choice:** preserve the exact allowance and native mechanics. Continue legitimate exploration/acquisition; record crafting unavailable until a legitimate workbench and execution path exist.

**Rejected:** an extra table in the bootstrap, a free crafting API, player crafting disguised as robot autonomy, or a fabricated crafting provider.

**Verified:** installed static recipe/API inspection and a real isolated turtle probe. The first probe failed because it called an absent function; that failure was retained. The corrected probe reported the absence explicitly.

**Consequence:** first crafting infrastructure has not been demonstrated. A naturally discovered workbench may offer a legitimate future route, but its discovery, acquisition and use are not assumed. Changing the bootstrap or mechanics requires a separate human rule decision.

## T03-ADR-004 — Version portable software without inheriting availability

**Choice:** allow explicit selection of the physically witnessed basic-extraction candidate in the clean package. The historical default remains available. Only portable source/static knowledge is copied; physical approvals, world state and infrastructure availability remain empty.

**Verified:** clean-package tests check both the unchanged default and the explicitly selected candidate. Trial 03 started with zero inherited physical tables and its own independently observed equipment.

**Consequence:** each fresh run still requires its own commissioning, current recipe binding and observed capabilities. A software manifest is not physical evidence.

## T03-ADR-005 — Forward-reconcile only proven idle telemetry

**Context:** an isolated restart found a fully written next journal generation left as a temporary file. The robot had no pending job, but its recorded finite operating grant had only expired after that snapshot. The existing held-only repair correctly refused it.

**Choice:** add a separate audit-only validator: matching run/identity/epoch, exact next generation/digests, retired watermark, no pending work, telemetry-only changes, unchanged archived physical state and an expired matching immutable grant. Preserve both journal versions before a stopped-world forward rename.

**Rejected:** deleting the temporary file, accepting a checksum alone, weakening the held-only validator, replaying a command, or restoring an old database as though Minecraft had rolled back.

**Verified:** the audit and four unsafe variants, followed by a successful real restart. Six old acquisition commands stayed terminal; three new surveys overlapped natively for 14.744 seconds and retired with no claims.

**Consequence:** this remains explicit, narrow offline reconciliation, not a general automatic journal repair.

## T03-ADR-006 — Make safe hold close admission promptly

**Context:** the first Trial 03 attempt stopped scheduling with no active claims, but an empty current permit stayed active until its original expiry. Inspection disproved the initial suspicion of an asynchronous race: the code simply separated policy pause from admission expiry.

**Choice:** atomically pause scheduling/renewal and close new admission. Accepted commands retain their separate immutable execution leases. Operations still requires actual retirement and zero claims before recording a drained hold.

**Rejected:** forcing jobs terminal, revoking uncertain physical work, changing inventory, or bypassing reconciliation.

**Verification:** focused tests preserve accepted lease data, reject renewal after pause and keep Operations responsible for drain. Continuation 02 physically verified prompt drain of an empty window, with zero outstanding claims. Accepted in-flight lease preservation is software-tested; this new run is not evidence of interrupting a physical job.

**Consequence:** a hold becomes prompt for idle windows; ambiguous accepted work still requires proper reconciliation.

## T03-ADR-007 — Distinguish a search budget from an exhausted world

**Context:** Trial 03's first attempt completed 24 surveys, enlarged legitimate knowledge and retained healthy fuel. Its next blocker was the configured search ceiling. That did not establish that no useful frontier or resources remained.

**Choice:** preserve the original blocked root and all its jobs; permit a distinct broad continuation objective with at most 96 extended surveys. Children remain incremental, at most three surveys outstanding, with bounded request accounting, known-home limits, fuel reserves and a finite operating permit. Codex does not choose individual robot jobs or resource coordinates.

**Rejected:** relabelling a budget limit as completed progression, rewriting the first result, dispatching hundreds of speculative jobs, or increasing the native prospecting range.

**Software verification:** explicit 96/97 boundary tests, incremental-child deduplication and the complete regression suites. An initial synthetic test selected acquisition because its fixture supplied observed stone; it was corrected to an explicit non-resource fixture rather than weakening the exploration assertion.

**Actual outcome:** continuation 02 added 30 verified surveys, then hit the existing ledger child limit. The higher allowance did not fit the flat dependency tree. ADR-008 supersedes that request shape; the failed root and all physical evidence remain unchanged.

**Consequence:** a longer search can still fail. More mapped air is not resource production; the first-workbench boundary remains unchanged. The separate continuation result must be counted as an engineering-assisted trial, not uninterrupted autonomy.

## T03-ADR-008 — Budget the complete dependency tree before dispatch

**Context:** continuation 02 stopped at the unchanged 32-child ledger guard. A first independent batching test then exposed the unchanged 128-request-per-root guard. Both failed tests remain local evidence. Counting surveys alone ignored execution and Fleet descendants.

**Options:** increase global limits; special-case strategic roots; or retain the limits and admit small batches only when their full expected descendants fit.

**Choice:** reusable batches of at most three surveys. Every leaf retains its own execution and Fleet requests, native receipts and physical completion. The Director forecasts all three nodes per leaf and the batch wrapper. It stops with `OPENING_PLANNING_BUDGET_EXHAUSTED` before admitting work that cannot fit. The requested 96-survey ceiling is an upper bound, not permission to override the ledger. A pure three-wide search can fit 36 surveys in 121 requests, leaving the next ten-node batch inadmissible.

**Rejected:** changing the generic 32-child/128-root limits, deleting completed requests, silently creating replacement roots, claiming budget exhaustion proves no resources exist, or replaying old commands.

**Verification:** synthetic tests include execution and Fleet descendants, prove the 121-node result and unchanged 128-node rejection, and propagate blocked leaf evidence. These are simulated request tests, not Minecraft output. Continuation 03 physically completed 36 new surveys, preserving all 54 earlier jobs and receipts, then blocked at the forecast boundary. Final drain had zero claims. This verifies bounded execution, not unlimited strategy or resource acquisition.

**Consequences:** bounded strategic search remains a ceiling; a larger strategic lifecycle needs explicit design. Batch completion does not fabricate geological knowledge. Source changes can be reversed while keeping existing dependency/history records; physical effects cannot be rolled back by restoring a database.

## Regression and evidence discipline

The current continuation source passed **430 Node tests and all 30 PC suites including Lua**, plus **22 legacy/viewer suites including 30 viewer tests and Lua**. No suite was skipped. Earlier failures and each physical checkpoint were retained. The local structured journal records timestamps, evidence references, actual outcomes and reversibility; this public summary omits raw operational data.
