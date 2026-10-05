# PC Mission Control — Government, Architecture and Acceptance

5 October 2026 · Migration source baseline118 · Edge runtime10

**PC_MISSION_CONTROL_MIGRATION_COMPLETE**

**Post-publication finding:** the separately authorized [Trial 01](FRESH-WORLD-AUTONOMY-TRIAL-01.md) subsequently exposed missing fresh-run commissioning, broad opening-strategy and fresh viewer initialization. It stopped before operational dispatch. The development migration is accepted within the scope below; **fresh-world autonomy has not passed**. This is not approval or evidence for the final filmed run.

The applicable PC migration is accepted. Seven deterministic ministries now share one persistent PC ledger and one physical dispatch authority. Minecraft remains physical truth. The preserved development colony still contains the ten bootstrap robots; protected Iron Supply, Movin’ Around and flint preparation remain unsubmitted. A disposable fresh-start trial is a separate next phase, not evidence claimed in this report. The final filmed/YouTube run has not begun.

Acceptance means the supported paths were demonstrated, not that every Monifactory recipe can execute or that the colony is self-sustaining. Dispatch defaults to a safe hold. Explicit finite permits bound the active objectives, robot cohort, approved software, job count and expiry. Routine permitted operations require no Codex calls.

## 1. Government and ownership

### Mission Control / Director

The Director owns strategic objectives, global priority, dependency routing, cross-ministry arbitration, strategic blockers and human gates. It translates supported root objectives into persistent requests and follows their evidence to completion. It does not decide every turtle movement, maintain a private inventory balance or magically execute unknown mechanics. The common scheduler arbitrates ministry work; Fleet is the physical allocation boundary. A root can remain blocked truthfully while unrelated safe work continues.

### Exploration Control

Exploration owns mapping, bounded frontier exploration, prospecting, geological evidence, resource discovery and discovery requests. **Exploration finds ore.** A shortage may produce a bounded search request. Only a physically inspected ore observation becomes an approved extraction target. A native prospecting clue is weaker evidence and never creates an invented ore cell, count or vein centre. Exhausting supported search returns an unknown-location blocker.

The installed hard-hammer compatibility bridge is a narrow capability of Exploration. A turtle must select a real supported GTCEu hard hammer and physically interact with the adjacent front/up/down face. The bridge reuses the legitimate native prospecting result and preserves tool/material geometry, direction and costs. Lua receives native categories and translated material/name expressions:

```lua
local result = hammerProspect.scan("front")
print(textutils.serializeJSON(result))
```

The successful result has `success` and `messages`; each message carries the native category and name expression, which may contain `translate` and `with`. Failure remains a negative/error result. It exposes no hidden coordinates, ore counts, vein centre, vein size, complete hidden blocks, configurable radius, seed, region files or arbitrary world-query API. The PC may attach the already-known sensor origin outside the native result; that is not an ore location. Unresolved expressions remain raw data.

Parity, range boundaries and failures were tested in disposable Minecraft. The exact intended installed bridge was separately verified by real development turtle Lua and the Exploration ministry. A strict integrated disposable chain additionally proved native scan evidence preceded physical ore confirmation and Mining work.

### Mining Control

Mining exploits legitimately discovered, approved deposits. It owns extraction plans, bounded/dynamic ore stock targets, depletion reporting and the extraction demand presented to Fleet. It cannot turn missing stock into hidden-world discovery. Insufficient known supply creates an Exploration dependency. Newly exposed blocks may be observed during extraction and returned for classification; they are not an authorization for unlimited blind mining.

### Production Control

Production owns effective installed recipe knowledge, bounded recursive requirements, crafting, supported furnace processing, intermediates, production queues and executable capability limits. Cycle/depth/node/alternative budgets prevent endless planning. Ingredient, tool, variant and output evidence matter; tool first-use metadata changes must be reconciled rather than ignored.

**RECIPE KNOWN** means static knowledge explains a method. **PROCESS EXECUTABLE** additionally needs physically available infrastructure, approved adapter/runtime, installed recipe binding, ingredients, safe access, power/fuel where applicable and evidence semantics. A placed furnace is not automatically a commissioned process. Arbitrary GT machinery, fluids/research/custom semantics remain explicit unsupported capabilities.

### Logistics Control

Logistics owns the persistent PC physical inventory model: container identities/generations, observed coordinates, access geometry, exact slots, item variants, quantities, reservations, transfers, custody, freshness, reconciliation, storage pressure, machine inventories and turtle cargo. **Minecraft is physical truth; the database records observed physical truth.** Intent does not subtract items or create output.

A transfer reserves eligible stock, records exact source observations and physical collection, tracks turtle custody, then verifies destination delivery before settlement. Multiple sources are supported. Competing requests cannot each allocate the same items. Protected quest holds cannot be used by unrelated jobs or selective rearrangement. Ordinary selective collection can temporarily rearrange a supported chest within one journalled transaction; interrupted uncertainty is preserved.

Ordinary adjacent inventories can refresh from authenticated complete observations. Claimed/busy inventories are excluded. Protected staging requires two independent agreeing witnesses. Five-minute freshness is finite: readiness may expire while the underlying reservation remains protected. Changed or ambiguous contents require reconciliation, never a guessed adjustment.

### Construction Control

Construction owns requested projects, portable templates, known site/access planning, material dependencies, placement/orientation and physical verification. Current physical scope includes reusable chest/storage and furnace construction plus supporting verified access. It neither builds arbitrary structures to appear busy nor claims terraforming exists. A planned instance is not infrastructure. Unexpected placement, blocked access or partial construction remains failed/partial until evidence resolves it.

### Fleet Control

Fleet owns dynamic robot allocation, availability, useful concurrency, fuel/reserves, maintenance/recovery, safe execution capacity and the commissioning/expansion interface. Membership is not permanently an array of ten. The ten current robots are bootstrap assets; Robot11 remains a legitimate technology target, not a migration deliverable fabricated with Creative resources.

Robot, cell, container and machine claims prevent incompatible work. Retirement acknowledgement is required before robot reuse. Productive, on-demand and reserve roles explain intentional idleness. Low fuel and unverified return access suppress work. Short bounded work finishes before reassignment; arbitrary dangerous preemption is not implemented.

## 2. Persistent request government

A representative supported dependency flow is:

```text
Director -> Construction -> Production -> Logistics / Mining
                                               -> Exploration
                                               <- discovery evidence
                                  Mining -> Logistics -> Production
                     Construction <- verified materials/output
Director <- verified completed structure
```

Requests have unique IDs, root and parent/child links, deduplication keys, owners, priorities, versions, states, blockers and evidence references. Plans and jobs are distinct from requests. Children have independent execution/result evidence; dispatch does not satisfy their parent. A repeated event or child request cannot create duplicate physics. Stale epoch/version proposals are rejected.

The physical dispatcher commits resource ownership, immutable work and authority before delivery. Turtles validate local state, perform bounded actions and journal receipts. Durable host acknowledgement and archive receipt precede retirement. A failed/uncertain action is reconciled before any fresh attempt; historical failures are retained.

An ordinary completed inspection may settle forward from an identical fresh drained observation without repeating the inspection. Protected inspection repair is separate and keeps its two-witness requirement. Matching contents, source identity, run/epoch, geometry and receipts are required; the original revision failure is not erased.

## 3. Standing work and useful concurrency

Persistent ministry policies retain timers/cursors across service lifetimes. Exploration considers useful bounded mapping/prospecting; Mining works toward justified stock; Production maintains supported buffers; Logistics reconciles storage and routes transfers; Fleet handles fuel, recovery and allocation. Construction is project-driven. Director provides strategic priority and human-gate awareness.

Explicit work outranks appropriate background work. Policies account for available and reserved stock, inbound supply, storage capacity, recent witnessed consumption, configured lead-time assumptions, fuel and robot availability. Targets and job generation are bounded. A robot can correctly be idle because demand is satisfied, fuel policy blocks optional travel or it is reserved for recovery.

The accepted continuous permit creates successive short windows through the same scheduler. It does not create a competing scheduler or automatically expand scope. The development acceptance completed four windows and two stock cycles with seven cumulative verified jobs and zero model invocations. A revision race was reconciled from physical evidence; six completed jobs were not repeated. Three useful simultaneous jobs and adaptive stock behaviour were separately demonstrated in disposable Minecraft.

## 4. Authority and trust boundaries

| Component | Authority |
|---|---|
| PC Mission Control | Global persistent models, SQLite, seven ministries, requests, recipes/quests, inventory accounting, planning, dispatch, historical projections |
| Minecraft gateway / ComputerCraft | Bounded execution delivery/validation, communication, immediate safety and recovery journals |
| Turtles | Physical interaction, local inspection, local safety, durable action evidence |
| Viewer | Read-only current and historical projections; no command authority |
| Codex | Exceptional strategic reasoning, unsupported-mechanic engineering and software development; not routine scheduling |
| Human | Challenge rules, quest submission/rewards, final-run approval and defined high-risk gates |

One PC authority epoch owns dispatch. The old in-game strategic scheduler is disabled and its excess global databases were archived/retired. The gateway persists epoch/sequence fences. Host restart defaults held and requires fresh observations; it cannot silently renew an expired permit. A stale host backup cannot roll Minecraft back. Recovery compares current receipts/reality and moves the ledger forward under a fenced process.

The browser never receives the operator secret. Operator writes use a narrow authenticated local endpoint and allowlisted schemas. Quest text, recipes, item names and telemetry are untrusted data. The PC writer is exclusive; database locks are not removed merely because a PID looks old.

## 5. Persistence, databases and history

Each run has a unique RUN_ID and source binding, separate SQLite ledger and authority epoch. Static knowledge is portable; physical availability is run-specific. Copying identity files deliberately cannot be detected by an imaginary hidden-world fingerprint: explicit branch/restore procedures and reconciliation are required.

The actual SQLite models include:

| Model | Stored meaning |
|---|---|
| Static catalog records/output indexes/quest edges | Recipes,911quests, capabilities/technology definitions, dependency graph |
| Effective catalog | Installed generated recipes, items/tags/fluids, serializer coverage, source fingerprints and execution witnesses |
| Run metadata | Run/source/pack binding, schema, authority epoch, mode, source status |
| Requests/dependencies/plans/policies | Intent, child graph, bounded plans, standing timers/cursors |
| Jobs/claims/outbox | Physical commitments, ownership and delivery |
| Containers/slots | Observed generation/revision, exact variants/counts, capacity, freshness/evidence |
| Reservations/allocations/custody | Protected and operational commitments; physical holder after movement |
| Providers/entities | Verified capabilities, robots, infrastructure, routes, fuel, operational typed state |
| Cells/deposits | Legitimately observed geometry and approved extraction evidence |
| Events/evidence/streams/acknowledgements | Deduplicated ordered observations, provenance, gaps and durable cursors |
| History/archive | Run/day-indexed checkpoints/deltas, semantic events and evidence |
| Tickets/invocations | Bounded manual Codex handoff and optional invocation records |

SQLite uses transactional WAL/FULL durability. No transaction stays open while a turtle travels. Low-volume typed models use keyed JSON payloads; the inventory and request hot paths are indexed tables. JSON files are immutable envelopes/exports, not another writable authoritative database.

Long history resides on the host. The edge retains only local identity/safety/execution and bounded unreconciled communication data. Retirement requires verified host archival/acknowledgement; uncertain evidence remains pinned. ComputerCraft quota was not raised as the migration strategy.

The existing Three.js viewer uses current PC projections and separate historical reconstruction. Day replay does not change current requests, reservations or robot state. Backward playback removes later discoveries; forward playback reveals recorded knowledge; LIVE resynchronizes current state. Development history begins at recorded day10, not fabricated day0. Observer receipt time is not asserted as exact discovery time. Daily summaries are derived locally from closed history; GitHub is not live telemetry transport.

Fresh initialization copies portable software, schemas, static catalogs, templates and approved bridge implementation, but no terrain, deposits, routes, container instances, inventories, robots, fuel, jobs, requests, reservations, approvals, physical capabilities, quest staging/completion or physical history. The final offline package has178 source files,911quests and18 bounded recipes, with every physical table empty. It cannot activate an existing save or overwrite a destination. Effective recipe knowledge must bind to the new runtime before execution.

## 6. Recipe and quest coverage

The final development export accounts for **70,357 recipes**:

- **51,592 parsed:**38,266 GT and13,326 standard layouts.
- **18,765 explicitly unsupported:**18,735 custom semantics and30 serialization errors.
- **10 native execution witnesses** match the bounded legacy recipes under exact bindings.
- The smaller legacy planner catalog contains18 recipes,8 capability definitions and21 technology records.
- The static quest catalog contains911 quests; IDs and dependency semantics remain intact.

Parsed does not mean executable. Whole laboratory/development catalog equivalence was rejected:18,197 differences were classified and none waived. Individual approved native witnesses govern execution. Reloading Minecraft produces a new effective generation requiring rebinding.

Quest preparation can recurse through production, logistics and staging, but unsupported tasks and unknown completion stay explicit. Existing iron/hook/flint staging was physically rechecked. Neither inventory presence nor a READY state is submitted/claimed completion. Human authorization is still required.

## 7. Fuel and sustainability

Final development sample:38,101 onboard movement units,320 emergency reserve and zero accepted movement commitments. PC-era verified actions accounted for102 consumed and0 replenished; earlier or unobserved expenditure is unknown. Two observed logs are not assigned a fuel conversion value without a same-run witness. Inventory fuel potential is counted once and cannot simultaneously fund crafting and refuelling.

Two disposable native spruce regrowth/harvest/replant cycles passed, with54 physical jobs,12 logs harvested,1 sapling recovered,3 replants,1 native log refuel yielding15 movement units and11 logs delivered. That fixture used accelerated random ticks and inherited test equipment. Movement consumed24 units and saplings fell8 to6. **Positive fuel/seed sustainability is NOT proven.** The verified mechanism is portable knowledge; the fixture’s stock, coordinates and infrastructure are not colony knowledge.

## 8. Recovery and operational evidence

Verified scopes include real host service restart, gateway/runtime restart preservation, lost acknowledgement/duplicate receipt protection, actual transfer followed by host failure, changed-source rejection, interrupted local journal reconciliation, stale-observation gates, authority mismatch and clean namespace isolation.

The stale-host test compared an old32-item balance with real24+8 custody after transfer. It preserved acknowledged evidence, required fresh physical observations and reconciled forward with zero new physical actions. The recovered candidate remained held; this is not permission to automatically reactivate an old epoch. Simulated packet ordering and fuzz tests are labelled separately from live network failures.

Final host restart preserved all ten poses/fuel/cargo and protected holds with zero additional jobs/claims. The final inspection passed while fresh; later expiry correctly made allocations/readiness require reinspection. Recovery never makes inventory permanently fresh.

## 9. Acceptance matrix

| Subsystem | Result | Evidence scope |
|---|---|---|
| Preservation/epoch handover | PASS | Real development, ten original robots, protected items, single authority |
| Seven ministries/request graph | PASS | Single-root13-job disposable chain plus separate development construction/prospecting |
| Inventory/reservations/logistics | PASS | Native transfers, exact slots/custody, competing reservation test, multi-source and protected witnesses |
| Crafting/furnace/construction | PASS supported paths | Native input-side/output chain and development furnace craft/build; arbitrary machines remain unsupported |
| Prospecting | PASS | Native parity/boundaries and actual development Lua/ministry result |
| Standing policies/concurrency | PASS bounded scope | Three concurrent useful jobs; dynamic stock; development4windows/2cycles/7jobs |
| Forestry/refuelling | PASS mechanism / KNOWN LIMITATION economics | Two accelerated native cycles; no positive sustainability claim |
| Recovery/restore | PASS tested cases | Real restarts/transfers and stale-host forward reconciliation; no duplicate physics |
| Thin edge/host history | PASS | Global legacy retirement archived; bounded edge journals and restart proof |
| Viewer/timeline | PASS | Actual browser historical day10/play to19/LIVE110, concurrent present policy evaluation |
| Catalog | PASS accounting / PARTIAL executability |70,357 accounted recipes,18,765 explicitly unsupported,10 native witnesses |
| Quest knowledge/preparation | PASS supported scope |911quests; staged requirements protected, submissions human-gated |
| Clean namespace | PASS offline isolation | Empty physical tables, no approvals, portable catalogs retained |
| Regression | PASS |28 PC suites/404Node cases plus22 legacy suites/28viewer; required Lua suites executed |
| Performance | PASS measured scope | Million-cell synthetic SQL/archive/Three.js, actual API/receipt latency; no exactTPS guarantee |
| Manual inbox/empty checks | PASS | Three actual empty scheduled checks, including regular ten-minute ticks; zero models |
| Automatic Codex invocation | UNAVAILABLE OPTIONAL FEATURE | Disabled; manual fallback only; no API-key/paid-provider workaround |

Local final tracker:166 requirements,165 VERIFIED,1 explicitly optional/unavailable;34 applicable acceptance scenarios PASS and1 optional unavailable. Original failures remain evidence, including furnace access, tool metadata, revision races and initial environment blockers. Later acceptance does not rewrite those failures as successes.

## 10. Operator and future-session runbook

Start the existing bound PC service with its documented `start.ps1`; use the pinned Node24.19.0 runtime. Inspect `health`, `observations`, `requests`, `operations`, `inventory`, `fuel` and current catalog before dispatch. Viewer is local loopback port4318; the structured versioned API is port4319. The UI is read-only. No secrets or raw runtime paths are published here.

For work, submit a supported strategic request, then an authenticated finite permit with exact run/epoch, roots, cohort and budgets. Current approved runtime and recipe witnesses are mandatory. Inspect explicit blockers rather than forcing work. `pause` stops admissions, `safe-hold` fences scheduling; drain/reconcile accepted work before `stop`. Do not blindly interrupt a turtle carrying unresolved custody.

After a service or Minecraft restart, wait for authenticated fresh observations and recipe-generation binding. Never replay a completed job because its parent was stale. Use receipt-only settlement where its exact guarded preconditions hold; otherwise new bounded reinspection, preserving the failure. Do not rerun already-applied handover or legacy retirement scripts.

A consistent final local ledger backup, source ZIP/SHA manifest, deployed-runtime fingerprints, original closed-world archive, physical receipts and complete requirement/evidence trackers are retained privately. Database migrations001/002 and current-source test harnesses are documented locally. The public repository remains documentation-only.

The ten-minute checker remains disabled/manual-only. Authentication investigation is closed. An empty inbox causes zero model invocation; deduplication, human-ticket separation and budget/error gates remain. Normal ministries do not require the checker or Codex.

## 11. Next phase and remaining gates

The migration is accepted; the next authorized experiment is a new disposable clean-start trial after this report is safely published. It must use a new RUN_ID and portable knowledge only, record history from initialization and preserve ordinary failures rather than manually manufacturing success. It is not the final filmed colony.

Quest submission/rewards, final-run activation, challenge changes, hidden terrain inspection and post-bootstrap spawning remain prohibited without their separate human authorization. Robot11, broader industrial processes and sustainable fuel are honest technology/policy work ahead. A successful migration supplies the evidence-based government needed to study those problems; it does not assert they are already solved.
