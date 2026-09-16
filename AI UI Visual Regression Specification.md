# AI UI Visual Regression Specification

Purpose: specification is not proof. The UI Construction and Visual Style Bibles must be validated against the actual Roblox Studio result.

## Required test viewports

- 1920×1080 desktop
- 1280×720 desktop
- 768×1024 tablet
- 375×812 mobile

## Structural checks

- ScreenGui hierarchy
- DisplayOrder
- AnchorPoint
- Position and Size
- AbsolutePosition/AbsoluteSize
- ZIndex
- UISizeConstraint
- UIAspectRatioConstraint
- Safe-zone compliance

## Visual checks

- no unintended overlap
- no off-screen controls
- no clipping
- no text truncation that changes meaning
- font availability confirmed
- typography hierarchy preserved
- panel borders/corners/backgrounds follow the Visual Style Bible
- required rarity/quality/status distinctions remain visually separable

## Interaction checks

- normal/hover/pressed/disabled states
- mobile hitbox minimum
- modal dim overlay
- risky modal cannot close via outside tap
- toast queue behavior
- responsive menu behavior

## Evidence

Every major screen requires screenshots at all applicable test viewports. A screen fails visual regression when any blocking requirement is not met.

## Output

```text
UI REGRESSION
SCREEN:
VIEWPORT:
PASS:
FAIL:
OVERLAP:
CLIPPING:
TEXT:
INTERACTION:
EVIDENCE:
STATUS:
```
