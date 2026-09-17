# Colony operations and fuel policy

Mission Control generates bounded useful work through its existing durable
objective lifecycle and job scheduler. The bridge and Three.js viewer remain
read-only. The local CLI submits strategy and policy; it does not drive individual
movement. The current implementation is a monitored development checkpoint,
not permission for unlimited unattended harvesting.

## Scheduling and ownership

CONFIGURE_OPERATIONS sets a run-scoped window (30–1800 seconds), a job allowance
(1–12), robot utilisation classes and an observed grove. It cannot import another
run's map or make an unknown resource location known. No clean world is started.
Three physical commands may execute concurrently. The manager considers measured
fuel demand, renewable stock shortages, useful ore cargo consolidation and bounded
frontier surveys. Existing PREPARE_QUEST parents retain their validated children;
strategic work pauses new background generation while short existing jobs finish.

Commands own their robot, inventory/machine and entire allowed travel corridor or
work area. Conflicting claims are rejected before dispatch. Claims survive restart
and remain held after uncertain execution. Workers use the claimed corridor rather
than taking shortcuts through their larger private map. Survey/forestry area claims
cover possible movement inside their bounds. Robot inspection and collision guards
remain active. There is no arbitrary physical preemption.

PRODUCTIVE robots receive useful bounded background work. ON-DEMAND robots remain
available for logistics or building. RESERVED robots retain recovery capacity.
The observer and headless operations view expose activity, intentional idle reasons,
blocked work, active jobs and reserve counts. Identity and role labels are preserved.

## Fuel and renewable stock

The controller measures changes in reported robot fuel. Consumption, replenishment,
measurement start, committed job estimates, fleet emergency reserve and estimated
runway are exposed. Earlier bootstrap expenditure is unknown. Fuel values per item
are recorded only after an actual refuel operation verifies them.

Initial policy retains 64 movement units per robot and a 640-unit fleet emergency
reserve. Each executor still validates its actual bounded outbound/work/return
budget. A distance-to-control estimate is explicitly labelled as a lower bound,
not a verified rescue route. Background work slows when measured burn exceeds
replenishment, and stops under low/critical fleet conditions. Zero-yield surveys
suppress further automatic surveys from that location. Active jobs finish safely
when the scheduling window expires.

The initial renewable target is 48 spruce logs. The manager leaves an eight-log
crafting buffer when generating ordinary refuel work. Installed pack knowledge
records that normal furnace charcoal is disabled; the loop does not assume a
vanilla charcoal recipe. Refuelling burns bounded quantities of legitimate carried
logs through turtle.refuel, measuring actual fuel and item deltas. Accepted fuel
commands reserve actual carried inventory through the existing reservation model.
Quest items are protected independently.

TEND_FORESTRY operates only at a registered, previously observed planting site.
It recovers leaves/saplings first, secures enough saplings before cutting additional
trunks, operates within movement/height/cargo limits and inspects replanted beds.
It returns through known space. Harvest output and replanting must be physically
verified; unsupported or failed regeneration remains a blocker.
After verified planting, another automatic grove check waits at least twenty real
minutes. At a previously renewed grove, the worker requires an observed trunk at
its approach before harvesting; immature saplings do not justify canopy traversal.
This cooldown limits inspection travel; it does not claim the tree has grown.

## Evidence and recovery

A delivery's inventory inspection can predate its return journey. For commands
holding exclusive inventory ownership, completion checks its job-attributed
inspection, source/destination quantity changes and actual return. A foreign
inspection cannot satisfy the command.

RECONCILE_DELIVERY is deliberately narrow: it validates a failed delivery whose
worker actually completed and returned, checks the same protected evidence and
fresh idle telemetry, and releases its quarantine without dispatching movement.
The original FAILED status and reason remain. Reconciliation is a new durable
command with its own evidence; no failed job is erased or retried blindly.

RECONCILE_FORESTRY similarly verifies the returned inventory of a partial attempt,
preserves its FAILED result and retains a repair requirement. The next grove job
can repair planting without harvesting again. It removes only inspected snow
layers from planting beds, then verifies every sapling individually. Renewal is
recorded only after the separate repair completes and the robot returns.

Long-term history remains in the local run-aware archive. The controller retains
32 recent full terminal jobs and six recent full terminal commands, plus all pinned
active/recovery/staging references and compact receipts. Full details are retired
only after verified host acknowledgement; this reduces storage pressure without
raising ComputerCraft's quota or discarding historical evidence.

## Current boundaries

This first manager has a small set of work generators, not a universal industrial
planner. It does not construct arbitrary machines, claim quests, find undiscovered
ore magically or rescue an unreachable robot automatically. Unsupported rescue,
new infrastructure and inaccessible fuel remain explicit development work. Its
initial operating windows are supervised and finite.
Carried-log refuelling is physically verified. Fuel delivery to another robot,
off-route rescue and efficient net-positive fuel production remain future work.
The first recovery of the partly harvested grove was fuel-negative; a successful
refuel does not establish colony-wide fuel independence.

All operating policy, locations, stock, fuel samples, reservations, attempts and
utilisation belong to the current RUN_ID. A new offline run inherits software and
static knowledge, but no operational state or assumed physical capability.
