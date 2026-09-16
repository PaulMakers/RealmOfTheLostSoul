# AI Map Visual Lint Specification

Purpose: prove that built map content actually matches the locked map layout and visual style documents.

## Object-level checks

For every building/prop group:

- correct name and parent
- correct position/rotation/footprint
- correct bounding box
- correct material/color
- correct building tier/style
- correct intended district
- anchored/collision state correct
- no unintended floating or intersecting geometry

## District-level checks

For each district:

- required buildings exist
- road access exists
- spacing and footprints match the construction spec
- decoration density matches the visual style rules
- district-specific visual identity is preserved

## Road checks

- endpoints connect to their intended nodes
- width matches primary/secondary designation
- no accidental dead gaps
- no unintended severe overlaps
- intersections remain traversable

## Terrain checks

- boundary is closed except specified openings
- no visible holes
- walkable paths remain walkable
- terrain materials match the intended region
- Part/Terrain transitions do not create visible seams

## Circular/curved geometry

- center/radius verified where specified
- segment continuity verified
- no major visible gaps
- radial orientation is continuous
- tool record confirms Launch Archimedes/PolyMap use when applicable

## Signage

Validate 3DText content, orientation, scale, readability distance, and clipping.

## Output

```text
MAP LINT
PASS:
FAIL:
BLOCKING:
AUTO-FIXES:
SCREENSHOT EVIDENCE:
TOOL EVIDENCE:
STATUS:
```
