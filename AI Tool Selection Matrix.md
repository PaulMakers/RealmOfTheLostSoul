# AI Tool Selection Matrix

This procedure is mandatory before building geometry, terrain, or UI.

| Requirement | Preferred tool | Manual construction allowed? |
|---|---|---|
| Gap/seam repair | Gapfill | Yes, only if tool cannot resolve it |
| Texture/surface treatment | AddEasyTexture | Yes, for unsupported/custom treatment only |
| Circle/arc/radial form | Launch Archimedes | Only if the required form cannot be produced by the tool |
| Organic terrain/cliff | Part to Terrain + Brushtool | Yes for small exceptions |
| Repeated modular objects | Redupe | Yes only for non-repeating exceptions |
| Custom footprint/silhouette | PolyMap | Yes if tool cannot represent required shape |
| Terrain painting/sculpting | Brushtool | Only if target operation is unsupported |
| UI construction | XieStudioUI | Manual fallback must be reported |
| Bulk replacement | ReplaceParts | Manual fallback discouraged; report reason |
| World signage | 3DText | Manual text geometry only if 3DText is unsuitable |
| Character/world animation | MoonAnimator | Manual animation fallback must be reported |
| Lighting/time animation | SunAnimator | Manual fallback must be reported |

## Decision sequence

1. Identify the exact shape or UI operation required by the source specification.
2. Search this matrix for the highest-level applicable tool.
3. Record `TOOL_SELECTED`, `REASON`, `INPUT`, `EXPECTED_OUTPUT`, and `VALIDATION_METHOD`.
4. Execute the tool.
5. Inspect the actual result.
6. Measure against the source specification.
7. Repair only the failed requirement.

## Mandatory examples

- Colosseum circular wall → Launch Archimedes before any manual segmentation.
- Curved road → Launch Archimedes or PolyMap.
- Organic cliff → Part to Terrain, then Brushtool.
- Repeated lamp/fence/window rows → Redupe.
- Building seam → Gapfill.
- City sign → 3DText.
- Bulk material swap → ReplaceParts.
- Complex UI screen → XieStudioUI when supported.

## Anti-pattern

Do not spend dozens or hundreds of manual Parts approximating a geometry that a designated tool can create directly, unless the tool was tested and documented as insufficient.
