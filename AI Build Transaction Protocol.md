# AI Build Transaction Protocol

Purpose: prevent failed or partial AI builds from leaving the project in a mixed or broken state.

## Transaction lifecycle

BEGIN STAGE
→ CREATE STAGING AREA
→ BUILD
→ INSPECT
→ VALIDATE
→ REPAIR
→ RE-VALIDATE
→ COMMIT or ROLLBACK

## Staging

Use a dedicated staging container such as:

```text
Workspace
└── _AI_BUILD_STAGING
    └── [Phase_Name]
```

Do not merge unvalidated work into production folders.

## Commit gate

Commit only when the stage has:

- expected objects
- expected dimensions/positions
- expected style/materials
- no Critical/Major failures
- required evidence captured
- validation report generated

## Failure handling

FAIL → isolate failed stage → repair → revalidate.

Do not continue to dependent stages while a blocking failure remains.
Do not silently delete or rebuild unrelated content.
Do not silently change design decisions.

## Recovery

If an operation leaves an invalid partial result:

1. Preserve the failure evidence.
2. Remove/revert only the affected staged content when safe.
3. Re-run the smallest failing operation.
4. Revalidate before merging.

## Commit record

Each committed phase should record:

PHASE:
SOURCE_SPECS:
TOOLS_USED:
OBJECTS_CREATED:
OBJECTS_MODIFIED:
VALIDATION_STATUS:
EVIDENCE:
NOTES:
