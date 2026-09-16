# Lost Soul — AI Execution Contract (Overview)

This is the entry point for every AI agent working on Lost Soul in Roblox Studio.

## Mandatory pipeline

SPEC → PLAN → TOOL SELECTION → BUILD → INSPECT → MEASURE → EVIDENCE → VALIDATE → REPAIR → RE-VALIDATE → COMMIT

## Core rules

1. Never treat successful script execution as proof of completion.
2. Read all relevant source specifications before modifying Studio.
3. Detect conflicts and ambiguity; never silently invent missing design decisions.
4. Use the designated Roblox Studio tool with the highest applicable abstraction level.
5. Use staging folders for atomic build phases.
6. Every phase must produce measurable validation evidence.
7. Visual work requires screenshots at the required viewport sizes.
8. Auto-fix only within the existing Guardrail whitelist.
9. Critical/Major failures block dependent phases.
10. No PASS or RELEASE READY status without evidence.

## Companion specifications

- `AI MASTER EXECUTION PROMPT.md`
- `AI Tool Capability Registry.md`
- `AI Tool Selection Matrix.md`
- `AI Build Transaction Protocol.md`
- `AI Evidence & Screenshot Protocol.md`
- `AI Cross Document Consistency Rules.md`
- `AI Map Visual Lint Specification.md`
- `AI UI Visual Regression Specification.md`
- `AI Performance Validation Specification.md`
- `AI Final Release Gate.md`
- `AI Validation & Guardrail Specification.md`

## Agent roles

Architect AI: interpret locked specifications and produce the build plan.

Build AI: execute the plan using Roblox Studio tools and staging.

Art Director AI: validate world/UI visual consistency.

UI Engineer AI: validate hierarchy, responsive layout, and interaction states.

QA AI: execute functional and structural validation.

Performance AI: validate instance count, lights, collision complexity, streaming, and runtime cost.

Final Auditor AI: verify all evidence and release gates.

No single agent may self-approve every role for a release candidate.
