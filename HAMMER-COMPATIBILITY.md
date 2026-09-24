# Hard-hammer compatibility proof

**RESULT: WORKS.** A real CC:Tweaked turtle Lua program received the same bounded message information as GTCEu's native hard-hammer prospecting calculation. This is an isolated prototype, not a Mission Control capability or deployment.

Tested with the installed Monifactory 0.13.7 gameplay files, Minecraft 1.20.1, Forge 47.4.13, GTCEu 7.5.3 and CC:Tweaked 1.116.1. The existing disposable Creative dedicated server was used. No development save was loaded.

## Implementation

The small Forge mod registers `hammerProspect` through CC's `registerAPIFactory`, only for computers with the `ComputerComponents.TURTLE` component.

`scan` queues work through `ITurtleAccess.executeCommand`. It requires a real GT `HARD_HAMMER` in the selected slot, with the actual `ProspectingBehavior` attached. It then executes **CC's existing `TurtlePlaceCommand`**. This retains normal item use, FakePlayer handling, protection checks, inventory loading/unloading, tool-state changes and turtle animation/command scheduling.

Two non-cancelling Mixin injections observe the installed `ProspectingBehavior.findOres`: entry checks that the native call targets the requested adjacent block and face; return captures the original message list. Neither injection changes arguments, scan results, range, costs or control flow. No scanning algorithm was copied. No extra scan is performed.

The capture is private to one synchronous server-thread operation and cleared in `finally`. Unrelated uses cannot retrieve another call's result. No stored scan cache or world database is created. Empty adjacent space is rejected rather than using CC's farther-block placement fallback.

This exact-version proof uses CC's internal placement class and runtime SRG names. Dependencies are pinned to the tested GT/CC versions. It is not a general compatibility release.

## Lua API and exact data

Select the slot containing the real hammer, then:

```lua
local result = hammerProspect.scan("front") -- also "up" or "down"
print(textutils.serializeJSON(result))
```

The tested magnetite result, with JSON key order normalized:

```json
{
  "success": true,
  "messages": [{
    "category": "ore",
    "name": {
      "translate": "tagprefix.stone",
      "with": [{"translate": "material.gtceu.magnetite"}]
    }
  }]
}
```

Every exposed field:

- `success`: whether a supported native interaction/result was obtained.
- `messages`: native message entries; empty when native GT returns no messages.
- `category`: exactly `ore`, `air`, `water`, `lava`, or `changing` (material change).
- `name`: ore entries only; the translation expression of the name GT actually displays.
- `translate`: that expression's translation key.
- `with`: optional nested translation arguments, needed for GT's prefix/material names.
- `error`: failures only, a fixed error code.

No messages are reinterpreted as deposit locations or vein estimates. Translation nesting is bounded and unexpected component forms fail closed. Vanilla copper's name is simply `{"translate":"block.minecraft.copper_ore"}`. An empty Lua message table may serialize as `{}` with CC's default JSON serializer.

Example failure: `{"success":false,"error":"MISSING_HAMMER"}`. Other tested failures were `WRONG_TOOL`, `INVALID_DIRECTION`, `NO_TARGET_BLOCK` and `INVALID_ARGUMENTS`. Item-use rejection, unexpected native output/context and queue failure also have fixed errors. The latter paths were inspected in code, not all independently triggered in-world.

**Not exposed:** hidden coordinates, distance, direction to ore, ore counts, complete block lists, chunk contents, vein center/size/metadata, seeds, region files or arbitrary world queries. There is no coordinate, radius, depth or remote-target parameter. The only direction parameter chooses the turtle's adjacent interaction face.

## Native comparison and boundary tests

For each of 17 fixtures, a fresh identical hammer was used first through ordinary `turtle.place*()` and separately through `hammerProspect.scan`. An opt-in lab logger captured GT's unmodified native message components at return for both calls. The test harness independently projected the ordinary native components into the documented schema and compared them against Lua, ignoring only message ordering. All 17 matched; the API never receives the logger's records.

| Test | Native and Lua result |
|---|---|
| Uniform stone / no ore | No messages; no false positive |
| Magnetite inside | Magnetite ore name |
| Magnetite beyond iron depth | No ore message |
| Copper inside | Copper ore name |
| Mixed targets | Magnetite, copper, air, water, lava and material change |
| Iron forward maximum / next step | Detected / not detected |
| Horizontal cross-section edge / next sideways step | Detected / not detected |
| Horizontal lower cross-section edge / next lower step | Detected / not detected |
| Up maximum / next step | Detected / not detected |
| Down maximum / next step | Detected / not detected |
| Steel forward maximum / next step | Detected / not detected |
| Iron at steel-only reach | Not detected |

Iron's tested depth is **5 steps including the clicked block**; steel's is **7**. The native cross-shaped sections, including the extra lower section for horizontal use, remain intact. The API contains neither range constant.

Six clean failure tests passed: empty selected slot, ordinary wrong item, GT pickaxe, invalid direction, no adjacent block, and extra coordinate argument. None invoked the prospecting calculation. Negative tests after positive scans also confirmed there was no stale result leakage.

The standalone `prospect.lua` program was executed by the real server-side turtle and returned magnetite successfully. No GUI interpretation or client player was involved. The oracle was the native calculation's returned messages, not a recreation of its world-scanning logic or a claim that every player GUI was exercised.

## Cost and performance

Iron and steel damage remained zero, item count remained one, and turtle fuel did not change. Native and compatibility calls produced identical full item-detail records before/after, including the opaque NBT hash. First use initialized GT's ordinary cached tool statistics identically; the bridge did not suppress or add this state change. These tested non-electric hammers consumed no energy.

Fifty consecutive successful calls took **19.650 seconds**; median call latency **400 ms**, mean **393 ms**, range **57–402 ms**. This includes CC command queueing and normal turtle animation, not just calculation CPU time. All results agreed and the already-initialized tool state stayed unchanged. Forge reported **20 TPS** before and after, with overall mean tick time approximately **0.51–0.55 ms**. No scan-induced freeze or crash was observed. Audit logging was enabled for this test.

## Files and reproducibility

Everything is under the local `investigations/hammer-bridge/` directory:

- `src/lab/hammerbridge/HammerBridge.java`: registration.
- `src/lab/hammerbridge/ProspectAPI.java`: validation and normal queued item use.
- `src/lab/hammerbridge/Capture.java`: bounded native-message projection.
- `src/lab/hammerbridge/mixin/ProspectingMixin.java`: entry/return observation.
- `resources/`: Forge and Mixin descriptors.
- `build.py`: Java 17-targeted compilation against the exact disposable installation; packages only this prototype's classes/resources.
- `build/hammerbridge-lab-0.1.0.jar`: tested local binary.
- `prospect.lua`: minimal working Lua program.
- `run_tests.py`, `test_runner.lua`, `benchmark.py`: disposable-only fixture harness.
- `paired-results.json`, `failure-results.json`, `prototype-result.json`, `benchmark-result.json`, `verification.json`: local evidence.

Tested JAR SHA256: `5c2010eae0f530f50f6703e3b6abc98d9f980f48c7e86ea2c83334fd366c7953`.

Compile from the project directory with `python investigations/hammer-bridge/build.py`. The launcher and fixture scripts are intentionally tied to the existing disposable laboratory. They must not be pointed at a real colony.

Early failures remain recorded: the first API returned CC's command-success prefix; the next guard checked a position local that GT had already advanced; the next encoder did not support GT's nested name expression. Those failed closed and were corrected before acceptance. A benchmark harness JSON serialization error caused by a shared table reference was corrected and the benchmark rerun. Startup-readiness handling was also corrected. None required a change to GT's prospecting algorithm.

## Development-colony boundary

The development run binding and all **693 compared ComputerCraft files** remained unchanged. Original installed source/configuration hashes still match the previous investigation. The prototype JAR is absent from the original instance's mods directory. No development robots were dispatched, no Mission Control software or state was changed, no quest was submitted, and no test-world fact was imported into colony knowledge.

The disposable server was stopped after testing. Source and binary remain local; only this mechanics report is suitable for the documentation repository. No Exploration Control integration or production deployment was performed.
