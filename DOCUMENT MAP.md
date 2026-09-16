# Realm of the Lost Soul — Document Map

This file is the quick-reference map for humans and AI agents.

## Authority matrix

| Domain | Primary authority | Supporting documents | Notes |
|---|---|---|---|
| Core game rules | `LostSoul.md` | city addenda, economy, NPC/quest docs | Master source for game-wide rules |
| Human City visual identity | `Map Visual Style Bible (Human City).md` | `Human City Build Package (A+B+C).md`, `Lost Soul City Content Addendum.md` | Visual/spatial rules live here |
| Human City construction | `Human City Build Package (A+B+C).md` | Human City visual bible | Construction package must respect the visual bible |
| City-specific content | `Lost Soul City Content Addendum.md` | `LostSoul.md`, NPC/quest, economy, UI docs | Additive unless an explicit override is stated |
| UI visual appearance | `Lost Soul — UI Visual Style Bible.md` | UI UX, UI Construction | Colors, typography, visual language, component style |
| UI/UX behavior | `Lost Soul UI UX Desain.md` | UI Style Bible, UI Construction | Flows, states, interaction intent |
| UI implementation | `Lost Soul UI Construction Specification.md` | UI UX, UI Style Bible, AI UI regression | Roblox hierarchy/layout implementation |
| Economy | `Lost Soul Economy Balancing.md` | `LostSoul.md`, city addendum | Numeric tuning authority |
| NPC dialogue / quest text | `Lost Soul NPC Dialog & Quest Text.md` | `LostSoul.md`, city addendum | Content authority for wording and quest text |
| AI execution process | `AI Execution Contract.md` | all AI companion specs | Controls how an agent works, not the game design |
| AI tool choice | `AI Tool Capability Registry.md`, `AI Tool Selection Matrix.md` | AI Execution Contract | Tool capability and selection |
| Atomic build/commit | `AI Build Transaction Protocol.md` | AI Execution Contract | Prevents partial/unsafe build phases |
| Evidence | `AI Evidence & Screenshot Protocol.md` | UI/Map/Performance specs | Proof requirements |
| Cross-document conflicts | `AI Cross Document Consistency Rules.md` | all design docs | Conflict detection/resolution procedure |
| Map validation | `AI Map Visual Lint Specification.md` | Human City docs | Geometry and visual checks |
| UI validation | `AI UI Visual Regression Specification.md` | UI docs | Responsive and visual checks |
| Performance | `AI Performance Validation Specification.md` | AI Execution Contract | Runtime and structural checks |
| Auto-fix limits | `AI Validation & Guardrail Specification.md` | AI Execution Contract | Whitelisted fixes only |
| Release gate | `AI Final Release Gate.md` | all AI validation docs | Final release criteria |

## Dependency direction

```text
GAME DESIGN
  LostSoul.md
      │
      ├── WORLD / MAP ──► Map Visual Style Bible
      │                     │
      │                     └──► Human City Build Package
      │
      ├── CITY CONTENT ──► City Content Addendum
      │                     ├──► Economy Balancing
      │                     ├──► NPC Dialog & Quest Text
      │                     └──► UI/UX updates where explicitly required
      │
      └── UI ──► UI Visual Style Bible
                 ├──► UI UX Desain
                 └──► UI Construction Specification

AI EXECUTION
  AI Execution Contract
      ├──► Master Execution Prompt
      ├──► Tool Registry / Selection Matrix
      ├──► Build Transaction Protocol
      ├──► Evidence Protocol
      ├──► Cross Document Consistency Rules
      ├──► Map Visual Lint
      ├──► UI Visual Regression
      ├──► Performance Validation
      ├──► Validation & Guardrails
      └──► Final Release Gate
```

## Reading order for a new AI agent

1. `README.md`
2. `LostSoul.md`
3. `DOCUMENT MAP.md`
4. The specialized specification for the task being performed.
5. Relevant AI execution/validation documents.

## Conflict rule

A document may only override another document when the override is explicit, scoped, and traceable. A filename or commit timestamp alone is not enough to establish authority.
