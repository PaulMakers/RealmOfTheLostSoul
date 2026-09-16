# AI Performance Validation Specification

Target: Lost Soul is designed around large maps and a 1000-concurrent-player target. Construction choices must therefore be checked for runtime cost as well as visual fidelity.

## Validate

- total instance count by district/building
- repeated object counts
- unnecessary loose Parts
- dynamic light count
- collision complexity
- streaming compatibility
- duplicated geometry that could use Redupe or reusable Models
- terrain vs Part choice for large organic surfaces
- UI update frequency and unnecessary per-frame work

## Tool-aware performance rules

Prefer:

- reusable modular Models over unique copies
- Redupe for repeated modular objects
- Part to Terrain for large terrain-like shapes
- ReplaceParts for controlled bulk changes
- grouped Models over uncontrolled loose Parts

Do not add high-cost decorative geometry merely because it is visually possible. The result must remain within the relevant performance budget in the source specifications.

## Output

```text
PERFORMANCE CHECK
SCOPE:
INSTANCE COUNT:
LIGHT COUNT:
COLLISION NOTES:
STREAMING NOTES:
TOOL OPTIMIZATIONS:
FAILURES:
STATUS:
```
