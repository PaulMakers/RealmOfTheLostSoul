# AI Cross Document Consistency Rules

## 1. Dependency lock

An AI must not start a build stage without reading the relevant upstream specifications.

### Map

Master Game Bible → Map/Construction specification → Human City Build Package → Map Visual Style Bible → Tool Selection Matrix → Build → Validation

### UI

Master Game Bible → UI/UX Design → UI Construction Specification → UI Visual Style Bible → Tool Selection Matrix → Build → Validation

## 2. Conflict detection

Before execution, check for conflicts in:

- coordinates
- dimensions
- object counts
- naming
- materials/colors
- hierarchy
- breakpoint behavior
- performance limits
- tool requirements

If two authoritative documents conflict, do not silently choose one. Report the conflict and block only the affected stage.

## 3. Derived values

When a value is derived from a source specification, record the formula or source section. Do not replace a derived value with an arbitrary approximation.

## 4. Change propagation

When a design document changes, identify all downstream documents that reference the changed requirement. Mark those areas as requiring revalidation.

## 5. Open decisions

Open design decisions must be explicitly marked. AI may build only the parts that do not depend on the unresolved decision.
