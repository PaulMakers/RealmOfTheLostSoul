# Lost Soul — Map Construction Specification

**Status:** Authoritative construction specification for the world/map layout.

## Purpose

This document locks the physical construction rules for maps. Visual appearance belongs to the applicable Map Visual Style Bible; city-specific additions belong to the City Content Addendum.

## Global Rules

- Use the coordinates and dimensions defined by the applicable build package when an exact value exists.
- Use the 4-stud construction grid for modular world elements unless an authoritative exception is explicitly documented.
- Do not invent new map nodes when content is defined as a sub-marker of an existing node.
- Any unresolved travel or layout decision must remain explicitly marked `OPEN DECISION` and must not be silently implemented.

## Human City

Human City construction is delegated to `Human City Build Package (A+B+C).md` after this specification establishes the map-level authority and dependency boundary.

## Validation

Before build, validate coordinates, dimensions, object counts, naming, materials, hierarchy, and performance limits against the authoritative upstream documents.

**Authority rule:** an explicit, scoped override in a higher-authority game/design document takes precedence over this generic construction guidance. Filename order and timestamps do not establish authority.
