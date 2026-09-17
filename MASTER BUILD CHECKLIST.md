# Realm of the Lost Soul — Master Build Checklist

**Branch:** `chore/reorganize-specs`
**Status:** Phase 0 audit in progress; Roblox Studio build not started.

## Phase 0 — Specification Consistency

### Authority / dependency baseline

- [x] README.md verified
- [x] DOCUMENT MAP.md verified
- [x] LostSoul.md verified as master gameplay/world authority
- [x] Map Construction Specification.md verified as authoritative construction specification
- [x] Canonical UI/UX document verified: `Lost Soul UI UX Design.md`
- [x] Legacy UI/UX filename retained only as compatibility stub
- [x] README/DOCUMENT MAP UI/UX authority references aligned to canonical filename
- [x] AI Execution Contract and Master Execution Prompt verified
- [x] AI Tool Capability Registry and Tool Selection Matrix verified
- [x] AI Build Transaction Protocol verified
- [x] AI Evidence & Screenshot Protocol verified
- [x] AI Cross Document Consistency Rules verified
- [x] AI Map Visual Lint Specification verified
- [x] AI UI Visual Regression Specification verified
- [x] AI Performance Validation Specification verified
- [x] AI Validation & Guardrail Specification verified
- [x] AI Final Release Gate verified

### Cross-audit / reconciliation

- [ ] LostSoul ↔ Economy cross-audit complete
- [ ] LostSoul ↔ Map specifications cross-audit complete
- [ ] City Content ↔ NPC/Quest ↔ Economy cross-audit complete
- [ ] UI/UX ↔ UI Construction ↔ UI Visual Style cross-audit complete
- [x] AI execution ↔ Tool Matrix ↔ Validation/Evidence pipeline cross-audit complete
- [ ] Full formula audit completed
- [ ] All worked examples reconciled against their formulas
- [ ] LUK/gold modifier examples reconciled
- [ ] EXP progression formula/target examples reconciled
- [ ] NPC buy/sell/fallback terminology normalized
- [ ] Gross/net shop examples reconciled
- [ ] Merchant Guild ROI example reconciled
- [x] Open Decision register created in `PHASE 0 AUDIT REPORT.md`
- [x] Every currently registered open decision has owner, scope, dependency impact, and status
- [ ] Phase 0 validation report updated after all reconciliation work

**Phase 0 status:** IN PROGRESS

**Current known audit findings:**
- Economy LUK formula is `1 + (Player_LUK × 0.1%)`; existing +10/+30 LUK worked examples are arithmetically inconsistent.
- 20 LUK on 3000 base gold/hour yields 3060 gold/hour under the stated formula, not 3006.
- `LostSoul.md` EXP examples yield ~6.7 min (Lv 1→2), ~20.5 min (Lv 5→6), and ~50.4 min (Lv 10→11), which do not consistently support its ~1 hour/level early-game claim.
- Economy contains multiple NPC buy/sell/fallback conventions that require terminology normalization before implementation.
- Merchant Guild ROI example states ~167000 gold of sales for a 5000g fee at a 2-point tax saving; simple breakeven is ~250000g, so the example requires correction or a defined alternative ROI method.
- City Content Addendum retains explicit open decisions for trainer placement, Colosseum footprint, quality probability curve, and related pricing confirmation.

**Phase 0 gate:** COMPLETE only when every required audit item above is PASS, all blocking conflicts are resolved or explicitly scoped, all open decisions are registered, and no Roblox Studio build/change has occurred before Phase 1 authorization.

## Phase 1 — Repository / Project Foundation

- [ ] Roblox project structure audited against repository naming/hierarchy rules
- [ ] Required foundation folders/configuration identified
- [ ] Server-authoritative foundation identified
- [ ] Content-data vs gameplay-logic separation planned
- [ ] Staging area created before build
- [ ] Validation evidence captured

**Dependency:** Phase 0 PASS

## Phase 2 — World / Map Blockout

- [ ] World boundaries
- [ ] Major map layout
- [ ] Cities
- [ ] Hunting Grounds
- [ ] Dungeons
- [ ] Roads/navigation
- [ ] Major landmarks
- [ ] Terrain/Part transitions
- [ ] Map lint + evidence

**Dependency:** Phase 0 PASS; applicable map specs PASS

## Phase 3 — Building Blockout

- [ ] Required building list verified
- [ ] Exterior/interior scope verified
- [ ] Footprints/dimensions verified
- [ ] Entrances/doors/windows/floors/walls/roofs verified
- [ ] Purpose and district membership verified
- [ ] Construction tools selected per matrix
- [ ] Building validation + evidence

**Dependency:** Phase 2 PASS; relevant building packages PASS

## Phase 4 — Player / Character Systems

- [ ] Race data/config
- [ ] Stats and progression
- [ ] Server-authoritative validation
- [ ] Character foundation

## Phase 5 — Combat System

- [ ] Server-authoritative damage
- [ ] Stats/formulas verified against source
- [ ] Skills/cooldowns
- [ ] Element interaction

## Phase 6 — Monster System

- [ ] Monster content data
- [ ] AI/aggro/leash/detection
- [ ] Combat behaviors
- [ ] Drops/EXP/gold sourced from specs

## Phase 7 — Item / Equipment / Weapon System

- [ ] Content data
- [ ] Equipment slots/attachments
- [ ] Stats/requirements/rarity/quality
- [ ] Economy integration

## Phase 8 — Inventory / Equipment UI

- [ ] UI UX flow
- [ ] UI Construction hierarchy/layout
- [ ] Visual Style implementation
- [ ] Required viewport validation

## Phase 9 — NPC System

- [ ] NPC content data
- [ ] Locations
- [ ] Dialogue source integration
- [ ] Shop/quest hooks

## Phase 10 — Quest System

- [ ] Quest data
- [ ] Five-state lifecycle
- [ ] Objectives/rewards
- [ ] Tracking UI integration

## Phase 11 — Path / Skill System

- [ ] Path data
- [ ] Hidden/evolution conditions from authoritative specs
- [ ] Skill progression
- [ ] UI integration

## Phase 12 — Economy / Shop / Trade / Crafting

- [ ] Economy formulas validated
- [ ] Shop/trade logic
- [ ] Crafting/quality tiers
- [ ] Server authority
- [ ] Economy examples reconciled

## Phase 13 — Dungeon System

- [ ] Floors/modifiers
- [ ] Entrance/telemetry
- [ ] Boss integration
- [ ] Loot/roll UI

## Phase 14 — Guild / Social System

- [ ] Guild data
- [ ] Bank/logs
- [ ] Chat channels
- [ ] Guild UI

## Phase 15 — PvP / Criminal / Bounty

- [ ] Server-authoritative rules
- [ ] Status/UI indicators
- [ ] Bounty/restriction integration

## Phase 16 — Colosseum

- [ ] Arena geometry via designated tool where applicable
- [ ] Bracket/betting rules from specs
- [ ] UI surfaces
- [ ] Validation/evidence

## Phase 17 — Complete Environment Art

- [ ] Decorative pass only after layout validation
- [ ] Terrain polish
- [ ] Repeated props via designated tools
- [ ] Signage via 3DText

## Phase 18 — Complete UI / UX

- [ ] Main HUD
- [ ] Menus and contextual windows
- [ ] Map/minimap
- [ ] Notifications
- [ ] Settings/accessibility
- [ ] PC/Mobile/Tablet validation

## Phase 19 — VFX / Animation / Audio

- [ ] Character/world animation via MoonAnimator where applicable
- [ ] Lighting/time animation via SunAnimator where applicable
- [ ] VFX/SFX validated against source scope

## Phase 20 — Optimization

- [ ] Instance counts
- [ ] Mesh/triangle/texture cost
- [ ] Lights
- [ ] Collision complexity
- [ ] Streaming
- [ ] AI update frequency
- [ ] RemoteEvent/UI update frequency

## Phase 21 — QA

- [ ] Structural validation
- [ ] Gameplay validation
- [ ] UI validation
- [ ] Cross-platform validation
- [ ] Performance validation

## Phase 22 — Cross-Document Audit

- [ ] Authority map rechecked
- [ ] Overrides traceable
- [ ] Derived values rechecked
- [ ] Open decisions accounted for
- [ ] No unexplained substitutions

## Phase 23 — Final Release Validation

- [ ] All required phases PASS / PASS_WITH_MINOR as allowed
- [ ] Critical failures = 0
- [ ] Major failures = 0
- [ ] Required evidence complete
- [ ] Map visual lint PASS
- [ ] UI visual regression PASS
- [ ] Performance PASS
- [ ] Final validation report generated
- [ ] Release gate evaluated

## Tool Decision Record Template

For each major construction operation:

- `TOOL_SELECTED:`
- `REASON:`
- `INPUT:`
- `EXPECTED_OUTPUT:`
- `VALIDATION_METHOD:`

## Phase Report Template

- `PHASE:`
- `EXPECTED:`
- `ACTUAL:`
- `TOOL:`
- `INSTANCE COUNT:`
- `FAILURES:`
- `AUTO-FIXES:`
