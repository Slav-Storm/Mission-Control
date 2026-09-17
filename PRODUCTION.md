# Production planning and quest preparation

Mission Control now has a bounded production planner inside its existing controller.
The local CLI submits planning requests through the same durable command interface.
The browser remains an observer, with no submission or execution channel.

## Knowledge and capability

The installed expert-mode configuration, KubeJS scripts and mod recipe definitions
provide a curated eleven-recipe catalog. It includes expert planks, sticks,
chests and furnaces, ordinary magnetite smelting, iron-furnace alternatives, an
assembler recipe and wooden grappling-hook components. Source hashes are recorded
locally. Generated recipe IDs and unverified timing remain unknown where unresolved.
This is not a complete runtime recipe registry or a replacement for JEI.

Recipe existence and process availability are separate. Capabilities derive from
robot reports, successful physical operations and known infrastructure. A powered
assembler recipe is known, but no assembler is available. Acquisition coordinates
come exclusively from robot observations; static recipes provide no locations.

## Planning without physical execution

The existing local agent supports:

```text
node viewer/agent.mjs recipes [ITEM]
node viewer/agent.mjs plan-production ITEM QUANTITY
node viewer/agent.mjs plan-quest QUEST_ID
node viewer/agent.mjs command COMMAND_ID
node viewer/agent.mjs plans
node viewer/agent.mjs colonyCapabilities
```

Planning returns a durable command receipt. Query that ID for the controller's
actual result. PLAN_PRODUCTION and PLAN_QUEST record lifecycle history but create
zero physical jobs. Material plans are advisory; execution separately validates
the assigned robot, actual input access, reservations and return fuel.

Plans recursively allocate last-reported available stock, subtract reservations,
round recipe batches and expand ingredients and fuel. They include the dependency
tree, alternatives, provenance hash and structured blockers. Shared quest ledgers
prevent the same available stock satisfying multiple requirements. Bounds are
12 recursive levels, 160 expanded nodes and 40 alternative branches. Cycles,
unknown recipes, unknown resource locations, missing processes, unsupported
executors, fluids and tool configurations remain explicit blockers.

The existing 911-quest catalog and dependency graph remain intact. The first
controller preparation manifests cover Iron Supply, Movin' Around and Furnace v2.
Other catalog quests remain queryable; unsupported controller manifests return
QUEST_MANIFEST_NOT_INSTALLED rather than invented requirements or completion.

## Supported physical execution

PRODUCE_ITEM compiles supported recipe trees into sequential child jobs. Each
child verifies actual output, and the parent requires the final inventory delta.
The installed shaped grids now support multiple ingredient types and exact batch
quantities, including the wooden pickaxe, chain and hook. A pickaxe used in the
hook recipe is a consumed component; no reusable-tool behavior is invented.

Selective inventory access gathers exact unreserved ingredients across stacks.
It can temporarily buffer an unrelated first-slot stack in a robot when the chest
is full, then physically restore it. Reserved item types are never moved by the
selector. DELIVER_RESOURCE and COLLECT_RESOURCE use observed routes and verify
both source/destination inventory changes. Production still requires a verified
crafting robot facing an existing chest; arbitrary machines and remote
storage-to-storage ingredient collection remain unsupported.

Physical inventory and planned recipe surplus are separate planner fields.
A leftover plank expected from an earlier recipe is not treated as existing stock
or a resource that a courier can collect before that recipe executes.

The previously verified furnace iron path remains supported. A bounded extension
can load carried raw magnetite into an actually empty furnace from its input port,
insert legitimate log fuel, wait for real output, collect it from below and return.
Known-source acquisition can extract one specifically observed ordinary magnetite
block without entering the mined space. These operations use existing movement,
worker safety checks, scheduler ownership and completion evidence.

No dispatch is replayed blindly after a crash. An interrupted physical job requires
reconciliation. Browser or bridge failure cannot dispatch, cancel or alter jobs.

## PREPARE_QUEST boundary

```text
node viewer/agent.mjs prepare-quest QUEST_ID
```

PREPARE_QUEST now orchestrates a bounded sequence of validated child commands.
It rechecks the quest, reservations and current inventory after each completed
child. Supported actions include ingredient delivery from robot cargo, clearing
crafting-buffer space into courier inventory, production, staging and reservation.
Each child has its own durable lifecycle and parent link. The parent cannot
complete until physical staging verification reports READY FOR SUBMISSION.

There are at most 24 child commands, and an individual production request is
bounded to 16 requested outputs plus each adapter's batch limit. A failed or
rejected child stops preparation with a structured blocker; it is never blindly
retried. Unknown recipes/resources, unavailable infrastructure, unsupported
requirements and unverified prerequisites remain blockers.

Movin' Around now reached READY FOR SUBMISSION through this orchestrator. Three
collection children preserved chest overflow in a courier, a production child
executed six physically verified crafting jobs, and a staging child verified and
reserved one wooden hook. The quest remains unsubmitted and unclaimed.
See [the capability-development checkpoint](CAPABILITY-VERIFICATION.md).

Iron Supply's 24 ingots remain physically staged and reserved. Reservation records
never become ordinary available stock merely because verification ages. Readiness
expires to STAGED after five minutes; a fresh robot inspection can restore READY
FOR SUBMISSION. Quest submission, manual checkmarks and rewards remain subject to
explicit human authorization. No automatic quest claiming has been added.

## Storage and isolation

The authoritative plan lives once in its command record. `/api/v1/state/plans` is
a read-only projection; `/api/v1/recipes` serves static knowledge. No second
controller, scheduler, map or inventory database was introduced.

During this stage, growing state exposed the existing ComputerCraft disk quota:
the old save rotation temporarily required three full state copies. Rotation now
retires the previous backup before writing the replacement while retaining the
current state, or retains the backup when it is the only valid copy. Interrupted
writes and renames are tested. Quotas were not increased and command history was
not discarded. Run-scoped host archives now retain long-term records, with acknowledged
compaction and bounded recent ComputerCraft history. Current state, active work,
reservations and recovery evidence remain authoritative in Mission Control.
This remains a finite disk budget, not unlimited storage.
