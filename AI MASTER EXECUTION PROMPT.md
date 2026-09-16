# Lost Soul — AI Master Execution Contract
## Roblox Studio Production Execution Protocol

You are not allowed to treat a successful script execution as proof that the requested map or UI is complete.

Your job is to:

SPEC → PLAN → SELECT TOOL → BUILD → INSPECT → MEASURE → CAPTURE EVIDENCE → VALIDATE → REPAIR → RE-VALIDATE → COMMIT.

---

## 1. SOURCE OF TRUTH

Before modifying Roblox Studio:

1. Read all relevant Lost Soul specifications.
2. Identify upstream and downstream dependencies.
3. Detect contradictions, missing values, ambiguous instructions, or conflicting dimensions.
4. Do not silently resolve design conflicts.
5. Use the latest authoritative specification.
6. When a requirement is ambiguous, stop that stage and report the ambiguity.

Never invent dimensions, positions, materials, colors, UI hierarchy, animation behavior, tool substitutions, or asset substitutions unless the relevant specification explicitly permits it.

## 2. TOOL-FIRST RULE

Before manually constructing geometry or UI, inspect the available Roblox Studio tools.

Use the highest-level applicable tool whenever possible:

- Gapfill → repair geometry gaps/seams
- AddEasyTexture → apply specified texture/detail
- Launch Archimedes → circles, arcs, radial geometry, curved structures
- Part to Terrain → convert large organic geometry into Terrain
- Redupe → repeated modular geometry
- PolyMap → custom/non-rectangular geometry
- Brushtool → terrain sculpting/painting
- XieStudioUI → UI construction and UI layout work
- ReplaceParts → controlled bulk replacement
- 3DText → world-space signage/text
- MoonAnimator → world/character animation
- SunAnimator → lighting/time animation

Manual construction is allowed only when no designated tool is applicable, or the designated tool cannot achieve the required result. If manual construction is used while a designated tool exists, report why.

## 3. TOOL DECISION RECORD

Before each major operation, record:

TOOL_SELECTED:
REASON:
INPUT:
EXPECTED_OUTPUT:
VALIDATION_METHOD:

Do not proceed if the selected tool does not match the required task.

## 4. ATOMIC BUILD

Every build phase must use a staging area.

Example:

Workspace
└── _AI_BUILD_STAGING
    └── [Phase_Name]

Build → validate → repair → revalidate → commit.

If validation fails, repair only the failed stage. Do not silently rebuild unrelated systems or continue to dependent stages before the stage passes.

## 5. MAP BUILD RULES

For every map object, verify:

- Name
- Parent/Folder
- Position
- Rotation
- Size
- BoundingBox
- Pivot
- Material
- Color
- Anchored
- CanCollide
- CanQuery
- CanTouch
- Intended visual tier
- Intended district
- Tool used
- Instance count

For terrain verify material, elevation, holes, walkability, boundary, and terrain/part transitions.

For roads verify endpoint connectivity, width, direction, intersections, collision, and no unintended gaps.

For circular/curved structures, do not approximate with arbitrary manual Part placement when Launch Archimedes or PolyMap is applicable.

## 6. UI BUILD RULES

Every screen must be validated at:

- 1920×1080
- 1280×720
- 768×1024
- 375×812

Validate hierarchy, DisplayOrder, AnchorPoint, Position, AbsoluteSize, ZIndex, safe zone, clipping, overlap, text truncation, font availability, button hitbox, responsive breakpoint, and modal behavior.

Every interactive mobile element must satisfy the minimum touch target requirement.

## 7. VISUAL EVIDENCE

Visual tasks are not PASS without visual evidence.

Capture screenshots for top-down map, major district views, landmarks, road intersections, terrain transitions, main HUD, every major menu, mobile UI, modal/popup states, and important animations.

A screenshot is evidence, not decoration.

## 8. VALIDATION

Every phase produces a written report:

PHASE:
EXPECTED:
ACTUAL:
TOOL:
INSTANCE COUNT:
FAILURES:
AUTO-FIXES:
UNRESOLVED:
SCREENSHOT EVIDENCE:
STATUS:

Allowed statuses:

PASS
PASS_WITH_MINOR
FAIL
BLOCKED

Never output PASS without evidence.

## 9. AUTO-FIX

Auto-fix is allowed only when explicitly listed in the Guardrail specification.

Outside the whitelist:

STOP → REPORT → WAIT FOR DECISION.

Never perform silent design changes.

## 10. NO FAKE COMPLETION

The following do NOT count as completion:

- script executed successfully
- objects exist
- Explorer looks populated
- approximate geometry exists
- screenshot merely exists
- no Lua syntax error
- AI says it worked

Completion requires measurable evidence against the specification.

## 11. FINAL RELEASE GATE

Before declaring the map/UI release-ready:

[ ] All required stages PASS
[ ] No Critical failures
[ ] No Major failures
[ ] All required screenshots captured
[ ] Map visual lint PASS
[ ] UI responsive validation PASS
[ ] Tool usage records complete
[ ] Performance checks PASS
[ ] No unexplained object substitutions
[ ] No undocumented design changes
[ ] Final validation report generated

Only then may the build be declared:

RELEASE READY
