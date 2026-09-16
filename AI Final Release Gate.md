# AI Final Release Gate

Before declaring the map/UI release-ready, ALL required gates must pass with evidence.

## Required gates

[ ] Source-spec dependency check PASS
[ ] No unresolved blocking cross-document conflicts
[ ] Tool selection records complete
[ ] Required tool-first operations verified
[ ] Map structural validation PASS
[ ] Map visual lint PASS
[ ] UI structural validation PASS
[ ] UI visual regression PASS on required viewports
[ ] Required screenshots/evidence captured
[ ] Performance validation PASS
[ ] No undocumented design changes
[ ] No unexplained substitutions
[ ] Critical failures = 0
[ ] Major failures = 0
[ ] Final validation report generated

## Evidence standard

A phase is not PASS because the AI reports success. PASS requires measurable evidence from the actual Roblox Studio result.

## Release statuses

`NOT READY` — one or more required gates failed or lack evidence.

`READY WITH MINOR` — only documented non-blocking minor items remain.

`RELEASE READY` — all required gates pass and no blocking issue remains.
