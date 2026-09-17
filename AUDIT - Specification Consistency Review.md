# Realm of the Lost Soul — Specification Consistency Audit

**Audit branch:** `chore/reorganize-specs`
**Audit date:** September 16, 2026
**Scope:** repository structure + cross-document consistency review
**Status:** First-pass audit; findings below are intended to be resolved before implementation.

## Executive summary

The specification set is substantially stronger than a typical early-stage Roblox game design repository: it has explicit source-of-truth concepts, atomic build rules, visual validation, responsive UI requirements, and release gates.

The main risk is no longer lack of documentation. The main risk is **documentation drift**: several documents refer to specifications that do not exist in the repository, some rules are duplicated with different ownership, and at least two numeric examples in the economy document are mathematically inconsistent with their own formula.

No gameplay rule is changed by this audit file.

## Findings

### F-001 — Missing Map Construction Specification
**Severity:** BLOCKER for map implementation

`AI Cross Document Consistency Rules.md` defines the map dependency as:

`Master Game Bible → Map/Construction specification → Human City Build Package → Map Visual Style Bible → Tool Selection Matrix → Build → Validation`

However, the repository tree contains `Human City Build Package (A+B+C).md` and `Map Visual Style Bible (Human City).md`, but no standalone `Map Construction Specification.md` (or equivalent file).

The Map Visual Style Bible also describes a previous/companion `Map Construction Specification` as the document that locks layout. This makes the dependency graph point to a missing authority.

**Required action:** either add the missing Map Construction Specification, or explicitly redefine the dependency so the Human City Build Package is the authoritative construction/layout specification. Do not silently choose between them.

### F-002 — UI Construction Specification contains stale document-state wording
**Severity:** HIGH

`Lost Soul UI Construction Specification.md` says the UI Visual Style Bible is "belum dibuat" (not yet created). The repository now contains `Lost Soul — UI Visual Style Bible.md`, and that document explicitly supplies the tokens referenced by the Construction Specification.

This is a stale status statement, not merely a stylistic issue. An AI agent could interpret it as permission to invent visual values.

**Required action:** change the wording to state that the Visual Style Bible exists and is authoritative for final visual tokens.

### F-003 — Economy LUK examples contradict the economy formula
**Severity:** HIGH / numeric correctness

`Lost Soul Economy Balancing.md` defines:

`Luck_Modifier = 1 + (Player_LUK × 0.1%)`

Under that formula:
- 10 LUK = +1%, so 900 gold/hour becomes 909, not 1800.
- 30 LUK = +3%, so 900 gold/hour becomes 927, not 3600.
- 20 LUK = +2%, so 3000 gold/hour becomes 3060, not 3006.

The worked example's `0.002` is also inconsistent with the stated `0.1% per LUK` rule; 20 LUK should produce `0.02`.

**Required action:** correct the worked examples or deliberately change the formula. The formula and examples must agree before economy tuning is considered locked.

### F-004 — Human racial bonus is not consistently owned
**Severity:** HIGH / design conflict requiring decision

`LostSoul.md` describes the Human racial characteristic as `+5% bonus EXP from quests`.

`Lost Soul Economy Balancing.md` describes a Human racial bonus as `+5% gold from all quests`.

These may be intended as two separate bonuses, but the documents do not clearly state that they are both active simultaneously. If only one was intended, they conflict.

**Required action:** explicitly define the Human quest bonus as either EXP-only, gold-only, or both, and assign the authoritative rule to `LostSoul.md` with the economy document referencing it.

### F-005 — UI filename contains a typo/inconsistent spelling
**Severity:** LOW

`Lost Soul UI UX Desain.md` uses `Desain` instead of the English `Design` used elsewhere in the repository.

**Required action:** rename to `Lost Soul UI UX Design.md` and update every reference. Do this as a repository-level rename so links do not silently break.

### F-006 — AI authority model needs one explicit ordering rule
**Severity:** MEDIUM

The repository has a useful domain authority matrix, but the AI execution documents also say to use the "latest authoritative specification". Timestamp/latest-commit language can conflict with domain ownership.

The correct rule should be: **domain authority first; explicit scoped override second; chronology only establishes which version of the same authoritative document is current.**

`DOCUMENT MAP.md` already moves in this direction and should become the canonical rule.

### F-007 — Tool registry / tool selection should be validated against actual available tools
**Severity:** MEDIUM / implementation dependency

The execution contract names tools such as `Gapfill`, `AddEasyTexture`, `Launch Archimedes`, `Part to Terrain`, `Redupe`, `PolyMap`, `Brushtool`, `XieStudioUI`, `ReplaceParts`, `3DText`, `MoonAnimator`, and `SunAnimator`.

The repository has a capability registry and selection matrix, which is good, but the final build pipeline should require a capability check against the actual Roblox Studio environment before treating a tool as available. The UI Style Bible already uses this kind of verification discipline for fonts.

**Required action:** ensure the Tool Capability Registry records availability/version/status, not merely intended tool names.

### F-008 — UI source-of-truth chain should be explicit
**Severity:** MEDIUM

The UI set is logically divided into behavior (`UI/UX`), construction (`UI Construction`), and appearance (`UI Visual Style Bible`). This is good, but the documents should explicitly state precedence for cases where a concrete implementation value appears in more than one document.

Recommended precedence:
1. UI/UX = behavior and required surface
2. UI Construction = hierarchy, geometry, breakpoints, interaction structure
3. UI Visual Style Bible = colors, fonts, visual treatment
4. AI validation specs = acceptance tests, not design overrides

### F-009 — Map visual style references an external Claude URL in its table of contents
**Severity:** MEDIUM / portability

`Map Visual Style Bible (Human City).md` contains table-of-contents links pointing to a `claude.ai` conversation rather than local section anchors.

This makes the repository less self-contained and can break for readers without access to that conversation.

**Required action:** replace external conversation links with local anchors such as `#principles`, `#palette`, etc.

### F-010 — Open design decision: fast travel
**Severity:** LOW / intentional open decision

The UI/UX document explicitly says fast travel remains undecided and therefore World Map UI cannot be considered final until the decision is made.

This is not an error. It is correctly identified as an open decision and should remain marked as such until resolved.

## What is already structurally good

- `README.md` and `DOCUMENT MAP.md` now provide a navigation layer.
- The AI execution pipeline correctly separates specification, tool selection, build, inspection, measurement, evidence, validation, repair, and commit.
- The map visual bible separates world-art appearance from construction/layout rules.
- The UI set separates UX intent, construction, and visual appearance.
- The release gate explicitly blocks release without evidence.
- The repository uses a dedicated branch/PR for this cleanup instead of silently modifying `main`.

## Recommended repair order

1. Resolve F-001 (missing Map Construction Specification).
2. Resolve F-003 (economy math).
3. Resolve F-004 (Human racial bonus).
4. Resolve F-002 (stale UI style-bible wording).
5. Resolve F-009 (external Claude links).
6. Rename F-005 and update references.
7. Formalize F-006/F-007/F-008 as repository-wide rules.
8. Run a second consistency pass after these changes.

## Audit conclusion

The repository should **not move directly into a large AI map/UI build yet**. The most important blockers are identifiable and fixable at the documentation layer. Once the missing map authority and numeric/design conflicts are resolved, the existing AI guardrail architecture can be used much more reliably.
