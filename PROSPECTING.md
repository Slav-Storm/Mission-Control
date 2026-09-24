# Can the robots become geologists?

**PARTIALLY.** In the installed Monifactory 0.13.7 / GTCEu 7.5.3 / CC:Tweaked 1.116.1 combination, **no tested handheld prospecting tool delivers its scan result to Lua**. Two narrower methods work: reading visible surface indicators, and reading the physical output of a powered ore miner. Neither is an autonomous, non-destructive underground scanner.

## What was actually tested

A separate local Creative server used the installed gameplay jars, configuration and KubeJS scripts, with controlled targets. No development save was loaded. Five client-only mods were excluded from the server copy; its Lost Cities spawn profile was disabled to permit a flat test world. No prospecting rules, ComputerCraft item-use tags or integration mods were added.

The test comprised 36 handheld scenarios / 396 API calls, six additional concurrent event-capture tests, five indicator scenarios, five powered-miner scenarios, physical miner-output collection and scanner inventory access. Targets included no ore, iron, copper, GT magnetite, mixed ores, and inside/outside-range placements. These were spawned test fixtures, not colony discoveries.

The development run binding and all **693 existing ComputerCraft application files compared unchanged**. No development robot, command, inventory, reservation, map or capability was modified. No quest was submitted. The development game remained closed.

## Results by method

| Method / installed ID | Activation by turtle | Machine-readable result | Range / precision |
|---|---|---|---|
| Iron hard hammer, `gtceu:iron_hammer` | `place`, `placeUp`, `placeDown` return `true` | **No scan result.** Identical returns and final item details across all ore scenarios | Source: material-dependent depth; iron has five depth steps from the clicked block, with a cross-section around each step. Reports ore/block categories, fluids or air, not coordinates |
| LV Ore Prospector, `gtceu:prospector.lv` | All three placement calls return `false, "Cannot place item here"` | None | Source: 5×5 chunk square around the player's chunk, full vertical chunk scan |
| HV Advanced Prospector, `gtceu:prospector.hv` | Same failure | None | Source: 7×7 chunks; ore and bedrock-fluid modes |
| LuV Super Prospector, `gtceu:prospector.luv` | Same failure | None | Source: 11×11 chunks; ore and bedrock-fluid modes |
| Portable Scanner / Debug Scanner, `gtceu:portable_scanner`, `gtceu:portable_debug_scanner` | Three placement calls return `true`; powered diagnostic use consumes charge | **No diagnostic text or prospecting result in Lua** | Inspects the clicked block/machine; this is not the electronic ore prospector |
| Surface indicators, e.g. `gtceu:magnetite_indicator`, `gtceu:copper_indicator` | No item activation needed: `turtle.inspect()` | **Yes:** block ID, material inferred from that registered ID, facing | Exactly the adjacent observed indicator. A geological clue, not verified buried ore or a vein coordinate |
| Electric Scanner machine, `gtceu:hv_scanner` | Inventory insertion and machine interfaces work | Inventory/progress/energy are readable; **no terrain scan API** | Research/copying processor. Its data sticks contain recipe research, not terrain surveys |
| Electric ore miner, `gtceu:lv_miner` | Lua `setWorkingEnabled(true)` controls the powered machine | **Yes:** real output items through `list()` and physical collection through `turtle.suck()` | Source: default radius 8, a 17×17 horizontal footprint below the machine. Output identifies mined material, not its original coordinates |

Mining hammers are distinct from **hard hammers**: the installed hard-hammer behavior contains prospecting; the mining-hammer behavior provides area mining. Other tool materials were not individually tested.

Electronic prospector ranges and intended GUI behavior are **installed-source findings**, not successful turtle scans. The ore GUI stores material/block entries by horizontal column; its ore payload omits exact Y coordinates. The prospectors also send player minimap information. Bedrock-ore mode is disabled by this pack's `doBedrockOres: false` setting.

## Why activation is insufficient

CC:Tweaked calls item-on-block use from `turtle.place()`. Its fallback air-use path is restricted to certain item types and the `computercraft:turtle_can_place` tag. The installed electronic prospectors are not enabled through that path. None of the six handheld items is a valid turtle upgrade: both equip methods returned `Not a valid upgrade`. Holding an item in the selected inventory slot does not equip a digging/attacking tool; all tested attack/dig variants reported no equipped tool.

The hard hammer's installed `ProspectingBehavior` computes categories but sends messages only when the level is **client-side**. The turtle executes server-side. Portable diagnostic scanners send messages to their player object; the installed integration does not relay those messages to Lua.

Concurrent event capture ran during the three placement calls and afterward. Only `turtle_response`, `task_complete`, `turtle_inventory` and `timer` events appeared. No chat, action-bar or scan event appeared. Item details, inventory, peripherals, files and analog redstone provided no alternate scan result. No GUI-reading bridge was added.

### Exact item-data findings

- Hammer: Lua's `nbt` hash changed from `0b23e388c144e119d7313d85e2b2d8a1` to `1055430e679b6e59b210ce0057215edc`, identically with and without ore. Raw diagnostic NBT showed only `GT.Tool: {}` becoming `{MaxDamage: 256, HarvestLevel: 2}`. `Damage` stayed zero. This is lazy tool-stat caching, **not scan data**.
- Charged LV/HV/LuV prospectors: charge and Lua item details remained unchanged after failed activation.
- Portable diagnostic scanner against ordinary stone: unchanged item details. Against an LV electric furnace: charge decreased **100000 → 99100**. Debug variant: **1000000 → 999100**. The changed hash therefore indicates charge consumption; it does not encode a geological result.
- `getItemDetail(slot, true)` exposes identity, count, display name, tags, applicable damage and an opaque NBT hash. It does not expose arbitrary NBT, computed tooltips or messages.

## The useful installed machine interface

Both tested GT machines exposed these methods:

```text
list, size, getItemDetail, getItemLimit, pushItems, pullItems,
tanks, pushFluid, pullFluid,
getEnergyStored, getEnergyCapacity, getInputPerSec, getOutputPerSec,
isActive, isWorkingEnabled, setWorkingEnabled,
getProgress, getMaxProgress, setSuspendAfterFinish,
setBufferedText, parsePlaceholders
```

The GT integration registers control, energy, workable, cover and monitor interfaces. It does not register a handheld ore-scan peripheral. `parsePlaceholders` requires a suitable monitor cover; calling it on the tested bare scanner returned `false, "invalid cover"`. It is not arbitrary world or item-data access.

A blank data stick was inserted into the Scanner using `turtle.drop()` and read through `list()` / `getItemDetail()`. Attempted extraction from that input interface via `pushItems` transferred **zero** items. This test does not establish unrestricted access to every machine slot or side. No research recipe was executed; static recipe behavior establishes that this machine researches items rather than prospecting terrain.

The powered LV Miner returned raw iron, raw copper and raw magnetite in their respective test cases. Empty and outside-radius cases produced no output in the bounded observation window. A turtle subsequently collected the actual magnetite output and verified the machine inventory became empty.

**Do not interpret empty miner output as a definitive negative scan.** The exposed generic progress/active fields do not provide a distinct, reliable ore-scan completion result. A real system must distinguish depletion, power loss, suspension, obstruction and full output. Mining is destructive and requires infrastructure; it is not a lightweight explorer sensor.

## Costs and practical search

- **Hard-hammer prospecting:** zero durability consumed in these tests; no energy requirement. The tested iron tool reports maximum damage 256. Replacing it uses the installed six-iron-ingot plus one-stick shaped hammer recipe. Repair is unnecessary for scanning alone; mining/crafting wear is separate.
- **Electronic prospectors:** source-defined charge capacities are 100000 / 1600000 / 1000000000 EU. At the installed 100% multiplier, their GUI drains 2 / 32 / 2048 EU per update, including while the GUI remains open after its scan. GUI scan advances one chunk per update. These costs were not measured through a functioning turtle GUI. They are rechargeable electric items, but charging infrastructure was not tested here.
- **Prospector replacement recipes:** installed `CustomToolRecipes` uses the `EPS / CDC / PBP` pattern: one emitter, one sensor, three plates, two circuits, one display and one battery. LV uses steel plates, a glass plate display and LV components; HV uses stainless steel and a screen; LuV uses rhodium-plated palladium and a screen. Battery alternatives exist. No pack-script prospecting recipe override was found. Portable Scanner uses the analogous MV/aluminium/screen recipe.
- **Visible indicators:** inspection consumes neither item durability nor turtle fuel. Travel still costs fuel. Indicators are enabled in installed configuration and included in installed vein definitions. Their positions provide a clue associated with generation; absence proves nothing. Do not assume every vein generates a surviving visible indicator or that a player-placed indicator proves buried ore.
- **LV Miner:** source-defined consumption is 8 EU per active mining tick, with installed mining interval 160 ticks. Actual total depends on operation/position, not a universal per-scan fee. The test used a spawned charged LV battery and a prepared energy buffer exclusively in the disposable world. No extra mining consumable was required in the successful test. Automation must provide legitimate energy and collect output in a real run.

**Best immediate method for future Exploration Control:** inspect surface indicators while traversing legitimately reachable ground, store material clues separately from verified deposits, consult static vein definitions, and then physically investigate. A negative inspection means only “no indicator in this adjacent cell.” Powered miners are useful later for acquisition and positive inventory evidence, not for proving empty terrain.

## Tested portable prototypes

`observe_indicators.lua` exports `scan("front" | "up" | "down")`. The front-facing path passed all five controlled scenarios. It reports `PROSPECTING_RESULT`, material clue and `buriedOreVerified: false`. Up/down entry points share the ordinary inspection API but were not separately acceptance-tested.

`miner_probe.lua` performs a bounded 1–30 second observation of an existing powered miner, tracks output deltas, restores its prior enabled state, and writes JSON. The tested ten-second invocation returned `POSITIVE_OUTPUT` with raw magnetite. No output returns `INCONCLUSIVE`. It requires exclusive inventory ownership during the observation and is not a production-ready operations-manager adapter.

`probe_all_events.lua` is the diagnostic item-use harness. None of these programs contains Mission Control networking or a development run identity. **Nothing was deployed to the colony.**

## Smallest possible compatibility addition — not implemented

For autonomous non-destructive hammer prospecting, a small compatibility mod could expose the normal hammer's category result to its turtle caller. It would have to preserve the installed tool check, clicked face, exact scan geometry, applicable costs and ordinary ore/fluid/air categories. Because the existing hammer emits client-only text, merely listening for server chat would not solve it: the result computation needs a constrained server-side hook.

Return only the normal categories, not positions, counts, vein metadata or arbitrary chunk contents. Reject calls without the real supported tool; add no range parameter or world-file access. Electronic prospector support would separately need the normal charging, modes and bounded GUI scan lifecycle. No such integration was installed or prototyped here.

Advanced Peripherals' optional pack recipe for `advancedperipherals:geo_scanner` is present, but its mod jar is **absent**. Installing it would change the available mechanics and is outside this investigation.

## Evidence and limits

`provenance.json` records exact installed source hashes. Local-only experiment records contain the API responses, raw diagnostic item comparisons, controlled fixtures and machine inventories; none are colony knowledge. `verification.json` records the result assertions and unchanged development-state comparison.

The dedicated-server test proves the turtle server-side execution path. It does not claim a human opened every GUI, that artificially placed ore creates natural vein metadata, that minimap packets are Lua-readable, or that a custom integration has already solved the remaining gap.
