# Realm of the Lost Soul — Progress Map, Bugs & Features

## Project
Anime Fantasy Medieval RPG built in Roblox Studio.

## Current milestone status
| Milestone | Status | Notes |
|---|---|---|
| M0 Environment & Tooling Verification | LOCKED (SYNCED) | Studio/bridge environment verified. |
| M1 Project Foundation | PRESENT (SYNCED) | Core project foundation exists. |
| M29 Monster Detection | LOCKED (RUNTIME-VERIFIED) | Server detects nearest valid monster within range and sends status data. |
| M30 Monster Status UI | LOCKED (RUNTIME-VERIFIED) | Tested positive target display and negative/no-target hide state. |
| M31 World Foundation | LOCKED (RUNTIME-VERIFIED) | Workspace world/map structure verified in Play. |
| M32 Main City | LOCKED (RUNTIME-VERIFIED) | MainCity and core city structures verified. |
| M33 Houses | LOCKED (RUNTIME-VERIFIED) | Six house/building entries verified. |
| M34 Guild | LOCKED (RUNTIME-VERIFIED) | GuildHall/GuildRoof verified. |
| M35 Roads | LOCKED (RUNTIME-VERIFIED) | MainRoadNS/MainRoadEW verified. |
| M36 Environment | LOCKED (RUNTIME-VERIFIED) | Trees/decor/environment structure verified. |
| M37 Decorations | LOCKED (RUNTIME-VERIFIED) | 32 trees and 4 lanterns verified. |
| M38 Weapon 3D Assets | IMPLEMENTED / RUNTIME-TESTED | Factory constructors work and persistent weapon templates were created. |
| M39 Skill Book 3D Assets | IMPLEMENTED / RUNTIME-TESTED | Factory bug fixed; seven runtime skill-book templates created. |
| M40+ Combat / AI / Quests / Persistence | NOT STARTED | Planned next phases. |

## Feature map
### Character setup flow
Loading → Race Selection → Weapon Selection → Element Selection → Skill Book Selection → Setup Complete / Gameplay.

### Setup rules
- Server-authoritative race, weapon, element and skill-book selection.
- Weapon choices are filtered by race.
- Element selection is race-aware.
- Light is excluded from runtime-selectable configuration.
- Skill books must match the selected element.
- Setup locks after successful completion.
- Starting weapon determines the initial Job through `JobMapping`.

### UI
- Central `UIStateManager` state machine.
- Loading, race, weapon, element and skill-book selection screens.
- Gameplay HUD, backpack, stats and monster status.
- Quest tracker, shop, dialogue, inventory, skill tree, minimap, tutorial and skill bar.

### World
- `Workspace.World`, `Map`, `NPCs`, `Monsters`, `Interactive`, `Spawn`.
- Main city with central plaza, roads, guild hall, houses/buildings, trees, lanterns and decorations.

### Assets
- `ReplicatedStorage.Assets.Weapons.WeaponFactory`.
- `ReplicatedStorage.Assets.SkillBooks.SkillBookFactory`.
- Persistent weapon templates: Sword, WizardStaff, SummonerBook, Arrow, Pickaxe, CraftingHammer.
- Persistent runtime skill-book templates: Wind, Fire, Water, Earth, Lightning, Nature and Dark.

## Bugs and fixes
### Loading screen stuck
- UI screens were under `PlayerGui.UI`, while controllers looked directly under `PlayerGui`.
- `UIStateManager` was a LocalScript even though controllers required it as a ModuleScript.
- Fixed `LoadingController` paths and replaced the legacy state manager with a ModuleScript.

### SetupStageChanged RemoteEvent misuse
- `SetupCompletionHandler` attempted to assign `SetupStageChanged.OnServerEvent = nil`.
- Removed the invalid assignment and retained a dedicated internal setup-completion RemoteEvent.

### Controller path errors
- Fixed Race, Weapon, Element and Skill Book controllers to resolve through `PlayerGui.UI`.
- Gameplay-related controllers still need an audit because earlier runtime logs showed the same direct-PlayerGui path error in HUD, Backpack, Stats, SkillBar, QuestTracker, SkillTree, Shop, Dialogue, Inventory and Minimap controllers.

### Race selection currently broken
- `RaceValidationHandler` correctly uses `RaceConfig.Races` and validates race IDs.
- `RaceSelectionController` dynamically creates race buttons.
- Latest runtime inspection found `ButtonContainer` present but containing zero race buttons, so Human/Elf/Dwarf/Demon are currently not selectable.
- This is the current highest-priority setup-flow blocker.

### SkillBookFactory color bug
- Fixed incorrect table unpacking that caused `Color3 expected, got table`.
- Wind, Fire, Water, Earth, Lightning, Nature and Dark constructors were runtime-tested successfully.

## Verification
- M29/M30 have positive and negative runtime verification.
- M31–M37 have runtime structural verification; visual/aesthetic review was not exhaustive.
- M38/M39 constructors were runtime-tested and reusable templates persisted.
- Complete setup-flow runtime verification remains pending.

## Next priorities
1. Fix race-button creation/initialization.
2. Runtime-test Race → Weapon → Element → Skill Book end-to-end.
3. Ensure setup UI closes cleanly after skill-book completion and Gameplay becomes visible.
4. Audit remaining gameplay UI controller paths.
5. Continue M40+ combat, AI, quests and persistence.

## Architecture
- Config: `ReplicatedStorage.Shared.Config`
- Services: `ServerScriptService.Server.Services`
- Setup handlers: `ServerScriptService.Server.Handlers`
- Client UI: `StarterGui.UI`
- Remotes: `ReplicatedStorage.Remotes`
