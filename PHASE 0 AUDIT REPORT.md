# Phase 0 — Specification Cross-Audit Report

**Branch:** `chore/reorganize-specs`
**Status:** IN PROGRESS
**Roblox Studio:** No build/change performed

## 1. Authority and dependency verification

### Verified

- `README.md` identifies the repository as the design/AI execution source of truth and defines the source-of-truth hierarchy.
- `DOCUMENT MAP.md` defines the authority matrix and dependency direction.
- `LostSoul.md` is the master gameplay/world authority.
- `Map Construction Specification.md` is the authoritative map construction layer.
- `Human City Build Package (A+B+C).md` provides exact Human City coordinates, modular construction rules, and build sequence.
- `Map Visual Style Bible (Human City).md` owns Human City world appearance.
- `Lost Soul UI UX Design.md` is the canonical UI/UX behavior document; the old `Lost Soul UI UX Desain.md` is a compatibility stub only.
- `Lost Soul UI Construction Specification.md` owns UI hierarchy/layout/breakpoints/states.
- `Lost Soul — UI Visual Style Bible.md` owns final UI visual tokens, typography, and styling.
- `AI Execution Contract.md`, `AI MASTER EXECUTION PROMPT.md`, Tool Matrix, Build Transaction, Evidence, Cross-Document Consistency, Map Lint, UI Regression, Performance, Guardrail, and Final Release Gate define the execution/validation pipeline.

## 2. Cross-document audit

### LostSoul ↔ Economy

**Result:** dependency is present and the economy explicitly references Master Bible concepts. Numerical reconciliation is **not yet complete**. Known examples requiring correction/review are recorded below.

### LostSoul ↔ Map specifications

**Result:** dependency chain is present. `LostSoul.md` owns world/map design, while the map construction and Human City build documents specialize layout/construction. No blocking authority conflict was identified in this pass.

### City Content ↔ NPC/Quest ↔ Economy

**Result:** cross-references are present and the three documents explicitly integrate profession, NPC, quest, pricing, quality, and Colosseum content. Several City Content items remain explicit open decisions and therefore cannot be implemented yet.

### UI/UX ↔ UI Construction ↔ UI Visual Style

**Result:** ownership is coherent: UX behavior → construction hierarchy/layout → visual tokens/style. Canonical filename is now used by repository navigation. Font availability remains a Studio-time validation gate; no silent fallback is permitted.

### AI execution ↔ Tool Matrix ↔ Validation/Evidence

**Result:** coherent. The mandatory pipeline is:

`SPEC → PLAN → TOOL SELECTION → BUILD → INSPECT → MEASURE → EVIDENCE → VALIDATE → REPAIR → RE-VALIDATE → COMMIT`

Tool selection is mandatory before construction, and PASS requires measurable evidence.

## 3. Formula/example audit findings

### Confirmed arithmetic inconsistency: LUK gold modifier

Economy defines:

`Luck_Modifier = 1 + (Player_LUK × 0.1%)`

Therefore:

- 10 LUK = +1%, not +100%.
- 30 LUK = +3%, not +300%.
- 20 LUK = +2%.

The current examples stating `+10 LUK: +900 gold/hour` and `+30 LUK: +2700 gold/hour` are inconsistent with the formula.

For the Rank C example with 3000 base gold/hour and 20 LUK, the formula gives **3060 gold/hour**, not 3006.

**Action:** reconcile these examples before Phase 0 completion. No gameplay implementation should encode the inconsistent example values.

### Confirmed arithmetic/pacing inconsistency: EXP progression

`LostSoul.md` defines:

`EXP per kill = Enemy_Level × 15`

and also claims early progression is approximately **1 hour per level**. The same document's validation table instead yields:

- Lv 1 → 2: 100 EXP / 900 EXP/hr = **~6.7 minutes**, not ~1 hour.
- Lv 5 → 6: 1,540 EXP / 4,500 EXP/hr = **~20.5 minutes**, not ~1 hour.
- Lv 10 → 11: 6,300 EXP / 7,500 EXP/hr = **~50.4 minutes**, which is near the stated target.

The document currently says the first-pass formula "roughly holds up" the ~1 hour claim, but the Lv 1 and Lv 5 examples do not support that statement. This is a source-spec reconciliation issue and must be resolved before implementation of progression pacing.

**Action:** decide whether the authoritative target is the stated time-per-level curve or the current EXP formula/table, then propagate the chosen authority to the worked validation examples. Do not silently change either design target during Phase 0.

### Other numerical reconciliation candidates

- Economy uses multiple notions of NPC buy/sell/fallback pricing. The labels and examples need one unambiguous direction: player buys from NPC vs player sells to NPC.
- The Equipment Pricing Curve is now described as an NPC fallback baseline with +20% markup, but the generic NPC Shop Pricing example still states an Iron Sword NPC Sell price of 600g while the City Content fallback convention makes the corresponding fallback purchase 720g. The distinction between generic base value, NPC buyback, and NPC fallback sale price must be explicit.
- Player Shop trader examples mix gross transaction value, post-tax proceeds, and comparison against NPC buyback value. Normalize each example so every value is explicitly gross, tax/commission, net proceeds, or NPC buyback/fallback value.
- Player Shop and Guild Shop examples are arithmetically consistent on commission (500→450; 850→807.5), but their "profit vs NPC" comparison depends on the NPC value convention and therefore remains semantically unresolved.
- Merchant Guild ROI example uses the 2 percentage-point tax saving correctly as a simple breakeven illustration: 5000 / 0.02 ≈ 250,000, **not 167,000**. The stated `~167000` figure appears to use the wrong percentage difference. This example requires correction or an explicit alternative ROI definition.
- The NPC fallback +20% markup, material price tables, Monster Meat/Gem tables, and Colosseum numbers are internally readable, but their exact authority relationship and worked examples should be locked before implementation where an older baseline example remains.
- Progression pacing examples and farming-rate tables should be checked together for unit/time consistency, without changing design targets during this audit.

## 4. OPEN DECISION register

| ID | Decision | Scope | Owner | Dependency impact | Status |
|---|---|---|---|---|---|
| OD-001 | Fast travel behavior between maps | UI + map traversal | `LostSoul.md` / relevant map authority | Blocks final fast-travel behavior only | OPEN |
| OD-002 | Chef trainer placement model: one NPC per city vs one roaming NPC | NPC + City Content | City Content Addendum | Blocks final Chef trainer placement/dialog integration | OPEN |
| OD-003 | Jeweler trainer placement model: one NPC per city vs one roaming NPC | NPC + City Content | City Content Addendum | Blocks final Jeweler trainer placement/dialog integration | OPEN |
| OD-004 | Final Colosseum footprint per city | Map geometry | Map/City Content authority | Blocks final Colosseum geometry/blockout | OPEN |
| OD-005 | Profession quality probability curve by Profession Level | Crafting/economy/UI | City Content + Economy | Blocks final quality-roll implementation | OPEN |
| OD-006 | Final confirmation of City Content NPC fallback price tables/markup as authoritative examples | Economy | Economy + City Content | Blocks unambiguous NPC pricing implementation | OPEN |
| OD-007 | Exact font availability in target Roblox Studio version (`PlayfairDisplay`, `Nunito`) | UI typography | UI Visual Style + Studio validation | Blocks typography application if unavailable | OPEN / runtime validation |

**Rule:** `OPEN` decisions must not be silently implemented. Only unaffected stages may proceed.

## 5. Phase 0 gate

**Current result: NOT COMPLETE.**

Blocking reasons are specification-audit issues, not missing-file dependencies:

1. LUK/gold worked examples require correction/reconciliation.
2. EXP progression formula/target worked examples require reconciliation.
3. Economy pricing examples require normalization of gross/net and NPC buy/sell/fallback terminology.
4. Merchant Guild ROI example requires arithmetic correction or a clearly defined alternative ROI calculation.
5. Explicit City Content open decisions must be registered and respected.
6. Final Phase-0 validation report must be updated after numerical reconciliation.

No Roblox Studio change is authorized by this report.
