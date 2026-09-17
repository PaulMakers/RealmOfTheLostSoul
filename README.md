# Realm of the Lost Soul

Roblox open-world fantasy RPG design repository.

## What this repository contains

This repository is the **design and AI execution source of truth** for Realm of the Lost Soul. It is intentionally documentation-first: gameplay rules, world/map specifications, UI specifications, economy, narrative content, and AI build/validation rules are kept here before implementation.

## Start here

### 1. Master game design
- [`LostSoul.md`](./LostSoul.md) — Master Game Bible. Core gameplay, progression, combat, skills, paths, world, maps, economy, NPCs, lore, and technical notes.

### 2. World and map design
- [`Map Construction Specification.md`](./Map%20Construction%20Specification.md) — authoritative map construction rules.
- [`Map Visual Style Bible (Human City).md`](./Map%20Visual%20Style%20Bible%20(Human%20City).md) — Human City visual and spatial rules.
- [`Human City Build Package (A+B+C).md`](./Human%20City%20Build%20Package%20(A%2BB%2BC).md) — Human City construction package.
- [`Lost Soul City Content Addendum.md`](./Lost%20Soul%20City%20Content%20Addendum.md) — City content additions and integration rules.

### 3. UI / UX
- [`Lost Soul — UI Visual Style Bible.md`](./Lost%20Soul%20%E2%80%94%20UI%20Visual%20Style%20Bible.md) — Visual language for the UI.
- [`Lost Soul UI UX Design.md`](./Lost%20Soul%20UI%20UX%20Design.md) — canonical UX flows and screen behavior.
- [`Lost Soul UI Construction Specification.md`](./Lost%20Soul%20UI%20Construction%20Specification.md) — Implementation-level UI construction rules.

### 4. Economy and content
- [`Lost Soul Economy Balancing.md`](./Lost%20Soul%20Economy%20Balancing.md) — Economy and balancing rules.
- [`Lost Soul NPC Dialog & Quest Text.md`](./Lost%20Soul%20NPC%20Dialog%20%26%20Quest%20Text.md) — NPC dialogue and quest text.

### 5. AI build, validation, and release controls
The files below define how an AI agent is allowed to work in Roblox Studio:

- [`AI Execution Contract.md`](./AI%20Execution%20Contract.md) — entry point and mandatory pipeline.
- [`AI MASTER EXECUTION PROMPT.md`](./AI%20MASTER%20EXECUTION%20PROMPT.md) — detailed execution contract.
- [`AI Cross Document Consistency Rules.md`](./AI%20Cross%20Document%20Consistency%20Rules.md) — cross-document conflict handling.
- [`AI Tool Capability Registry.md`](./AI%20Tool%20Capability%20Registry.md) — available Studio tools and capabilities.
- [`AI Tool Selection Matrix.md`](./AI%20Tool%20Selection%20Matrix.md) — tool selection rules.
- [`AI Build Transaction Protocol.md`](./AI%20Build%20Transaction%20Protocol.md) — atomic build/commit protocol.
- [`AI Evidence & Screenshot Protocol.md`](./AI%20Evidence%20%26%20Screenshot%20Protocol.md) — evidence requirements.
- [`AI Map Visual Lint Specification.md`](./AI%20Map%20Visual%20Lint%20Specification.md) — map geometry/visual checks.
- [`AI UI Visual Regression Specification.md`](./AI%20UI%20Visual%20Regression%20Specification.md) — UI visual regression checks.
- [`AI Performance Validation Specification.md`](./AI%20Performance%20Validation%20Specification.md) — performance checks.
- [`AI Validation & Guardrail Specification.md`](./AI%20Validation%20%26%20Guardrail%20Specification.md) — validation and permitted auto-fixes.
- [`AI Final Release Gate.md`](./AI%20Final%20Release%20Gate.md) — release-readiness gate.

## Source-of-truth hierarchy

When documents disagree, do **not** silently choose a convenient interpretation.

1. `LostSoul.md` is the master gameplay/world authority unless a more specialized specification explicitly owns the same decision.
2. Specialized specifications own their specific implementation domain:
   - Map geometry/visuals → Map Construction Specification + Map Visual Style Bible + Human City Build Package.
   - UI appearance → UI Visual Style Bible.
   - UI behavior/layout → UI UX Design + UI Construction Specification.
   - Economy numbers → Economy Balancing.
   - NPC/quest wording → NPC Dialog & Quest Text.
3. AI execution documents control **how** implementation and validation are performed, not what the game design should be.
4. Later addenda may extend an existing specification only where they explicitly state an override or addition. They must not silently redefine unrelated rules.

## Change protocol

Before changing a locked design rule:

1. Identify the owning document.
2. Check downstream references and dependent specifications.
3. Record the reason for the change.
4. Update dependent documentation in the same change set where practical.
5. Run the relevant validation checks before calling the change complete.

## Current cleanup branch

This branch (`chore/reorganize-specs`) is for documentation organization and consistency improvements. No game-design rule should be changed merely for formatting convenience.
