# AI Tool Capability Registry

This registry defines what each available Roblox Studio tool is for and is referenced by the Tool Selection Matrix.

| Tool | Primary capability | Required use cases |
|---|---|---|
| Gapfill | Fills gaps and adapts Part geometry | Wall seams, floor seams, connector gaps, small voids |
| AddEasyTexture | Applies requested texture/surface design | Final surface detailing after geometry is correct |
| Launch Archimedes | Creates circular/curved/radial geometry | Arcs, circular arenas, curved walls, radial layouts |
| Part to Terrain | Converts Part geometry to Terrain | Organic ground, cliffs, large natural forms |
| Redupe | Repeats/duplicates geometry | Lamps, fences, windows, stalls, repeated modular pieces |
| PolyMap | Creates custom-shaped geometry | Non-rectangular footprints and custom silhouettes |
| Brushtool | Paints/sculpts Terrain | Terrain material regions and organic surface polish |
| XieStudioUI | UI construction workflow | ScreenGui/panel/layout work where supported |
| ReplaceParts | Bulk part replacement | Controlled material/part/class swaps |
| 3DText | World-space text | Signs, labels, landmarks, directions |
| MoonAnimator | Animation authoring | Character/world animations and cinematics |
| SunAnimator | Lighting/time animation | Lighting or time-of-day animations when required |

## Tool-first rule

Use the highest-level applicable tool before manually recreating equivalent work. Manual construction requires a recorded reason when a listed tool is applicable.

## Validation requirement

Tool invocation alone is not proof. The output must be inspected and measured against the relevant source specification.
