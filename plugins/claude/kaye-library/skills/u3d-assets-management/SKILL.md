---
name: u3d-assets-management
description: Places Unity assets & folders across `Assets/`, so any file is found by asset type, domain & module without search
when_to_use: 'Creating, moving, importing any Unity asset, even when user never mentions folder: new script file, scene, prefab, audio clip, texture, animation. Triggers: "where does this go", folder layout, project structure, `Assets/`, import, organize'
metadata:
  version: 1.5.0
---

## Assets Management
Everything authored lives under one underscore-prefixed root named for the game, `Assets/_MyGame/`, sorting above Unity's own and vendor folders. Paths below are relative to it, and that prefix repeats on any folder that should lead its listing.
A file's path reads in up to 3 levels under the root, so any file is found without search:
- Asset Type: what the file is (`Scripts/`, `Prefabs/`), always present
- Asset Domain: which area of the game it serves (`Mobs/`, `World/`), optional
- Asset Module: which scene or subsystem owns it (`Spider/`, `MinigameRacing/`), the same name in every asset type
```
Assets/_MyGame/Scripts/Mobs/Spider/SpiderController.cs
Assets/_MyGame/Prefabs/Mobs/Spider/Spider.prefab
Assets/_MyGame/Textures/MinigameRacing/StartFlag.png
```
Name every asset file, folder, and GameObject per [Unity Naming](#unity-naming).
#### Asset Types
One level under the root:
- `Scripts/`: C#
- `Audio/`: music and effects, split into its own domains, per the audio-only domains below
- `Sprites/`, `Textures/`: 2D art, where split: `Sprites/` gameplay-facing, `Textures/` the rest
- `Animations/`: `.anim` clips, `.controller` graphs
- `Prefabs/`: prefabs, made per [Prefab Usage](#prefab-usage)
- `Scenes/`: `.unity` files, optionally nested by area (`Scenes/Minigames/`)
- `Materials/`, `Tilemaps/`: 2D and tilemap work
- `Meshes/`: 3D model and `.mesh` assets
- `Plugins/`
- `Settings/`: project-level `.asset` files
- `Localizations/`: locale and string-table assets
- `Shaders/`: `.shader`, `.shadergraph`, `.hlsl` files
- `Fonts/`: font files and their `.asset` font settings
- `Inputs/`: `.inputactions` assets
- `VFXs/`: particle systems and Visual Effect Graph assets
- `Timelines/`: `.playable` Timeline assets
#### Asset Domains
A domain folder sits between an asset type and its modules, gathering the modules of one kind (`Scripts/Mobs/Spider/`). Use one once an asset type holds several modules of that kind; leave a small asset type flat.
- reuse the same domain name in every asset type holding its assets, like a module name
- spell it out in [Pascal Case](#letter-case-pascal-case), never abbreviate
- plural for a domain holding many (`Mobs`, `Items`, `Cameras`), singular for a one-of-a-kind (`Player`, `World`, `UI`)
- place a module by what it does in play, so a thrown coconut goes under `Combat` or `Items`, not both
- add a domain only when it names one clear responsibility, decidable at a glance
Common domains:
- `Mobs/`: hostile creatures the player fights or avoids
- `World/`: the playable space and its scenery, from terrain and props to level logic
- `Cameras/`: camera rigs and their behaviours
- `Items/`: collectibles and carried things
- `Player/`: the player character
- `UI/`: screens, panels, and HUD
- `Combat/`: damage, health, and hit logic shared by everything that fights
- `Interactables/`: things the player activates, such as doors, levers, and chests
Audio-only domains, valid under `Audio/` alone and never elsewhere:
- `BGMs/`: background music tracks, module subfolders (eg `Audio/BGMs/Lv1/`)
- `SFXs/`: sound effects, module subfolders, or effect-family subfolders for effects spanning every module (eg `Audio/SFXs/PlayerHit/`)
#### Asset Modules
One short [Pascal Case](#letter-case-pascal-case) name per scene/subsystem, reused identically in every asset type holding its assets: the module name is the constant, the asset type changes around it. Spell it out, never abbreviate. Where modules form a family, the family word leads so the family sorts together:
- Family Member: `MinigameRacing`, `MinigameHiking`, `MinigameHideNSeek`
- Level: `Lv1`, `Lv2`, numbered rather than named
- Screen: `StartScreen`, `PauseScreen`, `SettingsScreen`, every full-screen interface taking the word `Screen`
- Standalone Module: `SaveSystem`, `Inventory`, sharing a name with nothing else
- `_Shared/`: the module slot taken by whatever no single module owns, sorting first on its underscore prefix
### {[Claude:Skill] Usage}
If needed, invoke `u3d-naming`, `u3d-pfb`, or `style-letter-case-pascal-case` skills via `Skill` tool.