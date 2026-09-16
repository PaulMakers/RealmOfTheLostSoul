# Realm of the Lost Soul — Master Build Checklist

**Branch:** `chore/reorganize-specs`
**Status:** Audit baseline prepared; Roblox Studio build not started.

## Phase 0 — Specification Consistency

- [x] README.md verified
- [x] DOCUMENT MAP.md verified
- [x] LostSoul.md verified as master gameplay/world authority
- [x] Map Construction Specification.md verified as authoritative construction specification
- [x] Canonical UI/UX document verified: `Lost Soul UI UX Design.md`
- [x] Legacy UI/UX filename retained only as compatibility stub
- [x] DOCUMENT MAP UI/UX authority reference aligned to canonical filename
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
- [ ] Full specialized-spec cross-audit completed
- [ ] Formula/example consistency audit completed
- [ ] Open decisions catalogued and dependency-blocked stages marked
- [ ] Phase 0 validation report generated

**Phase 0 status:** IN PROGRESS

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
- `UNRESOLVED:`
- `SCREENSHOT EVIDENCE:`
- `STATUS:`

## Current Open Decisions

- Fast travel behavior remains `OPEN DECISION` in the canonical UI/UX specification and must not be finalized until defined upstream.
