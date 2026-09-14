# Realm of the Lost Soul — Progression

## Checkpoint

**Status:** Baseline checkpoint committed before fixing remaining runtime UI errors.

### Verified Progress
- Initial setup flow is working end-to-end in Roblox Studio:
  - Race Selection → Weapon Selection → Element Selection → Skill Book Selection → Gameplay
- Race/weapon identifiers have been aligned to canonical IDs.
- Human initial weapon flow was verified with the corrected canonical IDs.
- UI controllers have been corrected to resolve screens under `PlayerGui.UI`.
- `UIStateManager` references in the affected controllers have been corrected to resolve from the nested `UI` container.
- `WeaponSelectionController` has the required `SetupStageChanged` reference.
- `RaceConfig` now uses canonical weapon IDs for allowed-weapon validation.
- `SkillBookConfig` includes descriptions for the available skill books.
- Initial elements are configured as Wind, Fire, Water, Earth, and Lightning, with Light reserved for future progression.
- `GameConfig` defines the initial setup stages and future element progression.
- Server validation handlers were aligned with the canonical config IDs and setup flow.
- A full positive-path runtime verification reached Gameplay successfully.

### Remaining Verified Runtime Errors
These are the next issues to fix; they were observed after starting Play mode and are intentionally left unchanged in this checkpoint:

1. **MinimapController**
   - `Players.<player>.PlayerGui.UI.MinimapScreen.MinimapController:25`
   - `camera.CFrame` errors because the expected `Camera` object under `MinimapViewport` is nil/missing at runtime.

2. **ShopController**
   - `ShopController:98`
   - An expected RemoteEvent/reference is nil when accessing `OnClientEvent`.

3. **InventoryController**
   - `InventoryController:110`
   - An expected GUI button/control is nil when accessing `MouseButton1Click`.

### Next Development Step
Fix the three remaining runtime errors above, then rerun Play mode and verify there are no repeated startup/runtime errors. Also verify that `Light` is hidden and rejected during initial element selection because it is reserved for future progression.
