# Infrastructure and fleet-expansion checkpoint

This is a development-colony checkpoint, not a completed Robot 11 milestone.
The original ten robots remain intact. No new world was started, no robot or
resource was spawned, and no quest was submitted or claimed.

## Physically demonstrated

- The colony manufactured two chests from legitimate spruce materials and flint.
- A builder placed and verified a bulk-storage node and a fuel chest. Total
  reported chest capacity increased from 27 to 81 slots.
- A generic courier objective moved 128 cobblestone into bulk storage.
- A second generic transfer collected three spruce logs from each of two
  separate inventories and delivered all six to the fuel chest. Both source
  decreases, the destination increase and the courier's empty return were verified.
- Both quest stores were reinspected: Iron Supply retains 24 reserved iron
  ingots; Movin' Around retains its reserved wooden hook. Both reached
  READY FOR SUBMISSION again, without submission or reward claiming. Readiness
  still expires to STAGED when its physical verification becomes stale.

## Reusable interfaces

The existing versioned command lifecycle and scheduler now support:

| Operation | Meaning |
|---|---|
| PLAN_CONSTRUCTION | Pure plan for a bounded chest-storage or fuel-chest template |
| BUILD_STRUCTURE | Validate known clear space, claim materials/access, place, inspect and verify |
| TRANSFER_ITEM | Transfer an exact quantity from a known source or ANY_VALID_SOURCE to known storage |
| PLAN_FLEET_EXPANSION | Inspect the installed robot component chain, fuel condition and commissioning blockers |
| EXPAND_FLEET | Validate a one-robot expansion; currently returns a structured blocker before manufacturing |
| RECOVER_STRUCTURE | Reinspect a supported failed placement and return the builder; retain the original failure |
| SERVICE_ROBOT / RETURN_ROBOT | Bounded recovery of a failed forestry-route robot through adjacent computer APIs and observed routes |

Construction templates and algorithms are portable. Built instances, access
points, inventory reports, claims and verification records belong to the current
run. Unknown terrain remains unavailable. Unknown computer telemetry cannot
silently add a fleet member; future commissioning must establish membership first.

Transfers claim source and destination inventories exclusively. Their contents
are unavailable to competing plans until completion or explicit reconciliation.
The current adapter conservatively refuses collection of a reserved item type,
even if additional units of that type exist. Initial couriers must have empty
cargo; requests are bounded to 256 items and known routes. These are deliberate
limits, not universal logistics support.

Storage pressure is derived from measured inventory capacity and occupied slots.
The initial high-pressure threshold is 85%; it creates a planning requirement,
not permission to construct arbitrary chests. After these transfers, reported
capacity was 81 slots with 25 occupied.

## Robot 11: real technology boundary

The installed Monifactory ComputerCraft compatibility script replaces the
ordinary turtle recipe. One normal turtle requires:

- One stainless-steel crate.
- One normal computer.
- One HV robot arm.
- One HV conveyor module.

That computer requires seven steel plates, an HV circuit-tag ingredient and a
computer monitor cover. The normal wireless modem requires MV emitter/sensor
components, steel bolts and steel plates. The installed disk-drive recipe also
uses MV/LV industrial components. The bounded recipe catalog now contains these
installed definitions with source hashes; unresolved component recipes, tags and
execution adapters remain explicit blockers.

The inspected installed GTCEu robot-arm definition also involves HV motors,
an HV piston, stainless-steel rods, gold cable and an HV circuit. This is a real
industrial progression chain, not an ordinary iron-and-redstone turtle recipe.

PLAN_FLEET_EXPANSION targets a fleet of eleven, but EXPAND_FLEET reports
FLEET_EXPANSION_BLOCKED with zero physical jobs created. Component production,
software commissioning and sustainable fuel capacity are not yet established.
No robot item has been crafted, deployed or commissioned. No operational robot
dock or fleet-expansion milestone is claimed. Replacement and expansion are
distinguished in the planning model; unlimited replacement is not implemented.

## Failures and recovery

Three physical-development failures remain in history:

1. A full crafting buffer could not temporarily accommodate its reserved first
   stack. The guard stopped before consuming inputs. Internal consolidation now
   frees an unreserved slot; the reserved hook stays inside its chest and returns
   to its original slot. Reserved iron was untouched.
2. The first chest faced the turtle's heading, contrary to the initial adapter
   assumption. Placement stopped at its orientation check. A separate recovery
   objective reinspected the actual chest and returned the builder. The corrected
   template then built the fuel chest successfully.
3. During a supervised operations window, forestry lost its claimed access route.
   A rescue robot travelled through observed space, verified the stranded
   computer's identity and serviced it. The robot then returned through a
   validated route with its cargo intact. The forestry failure remains recorded,
   and grove work is blocked pending access revalidation.

The same operations window completed two legitimate automatic refuels: eight
earned logs supplied 120 measured fuel. Cumulative measured consumption still
exceeds replenishment. Fuel independence is not claimed. Automatic generation
is stopped at the end of the bounded window; telemetry, scheduling, observer,
archive and daily recording continue running.

## Preservation and verification

An application-state and source checkpoint was taken before implementation.
Read-only acceptance checks confirm the development run identity, all ten robot
identities, prior job/command IDs, prior map-cell keys and both reservations.
All ten robots reported fresh idle telemetry after recovery. No graphical
Minecraft control was needed for this physical chain.

The existing observer displays the added chests through ordinary telemetry.
Day history before construction contains neither structure; later snapshots
record their observations and verified infrastructure. The viewer remains
read-only, and historical playback cannot dispatch work.

The regression suite covers isolation, the offline initializer, navigation,
crafting, furnace production, reservations, quest orchestration, operations,
fuel, storage, archives, command lifecycle and viewer/history protocols.
Additional tests cover multi-source transfers, construction proof, guarded
recovery, dynamic membership and unknown-space rejection.

Controller storage now excludes unused worker-only code. Portable deployment
removes comments/indentation conservatively while preserving source line
numbers and multiline literals. Full terminal detail is retained locally for
at most eight recent jobs and two recent commands, additionally bounded to
8 KiB per collection; active/recovery/reservation evidence remains pinned.
Compaction still requires a verified host archive acknowledgement. Journals
rotate at 8 KiB and are pruned only after archival verification. No disk quota
was increased and no authoritative world knowledge was discarded.

Detailed telemetry, coordinates, source and archives remain local. GitHub carries
this documentation and concise completed-day summaries separately.
