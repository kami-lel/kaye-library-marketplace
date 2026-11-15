---
name: u3d-naming
description: Names anything in a Unity project, code identifier or asset, so related things sort together & each name reads at a glance
when_to_use: 'Naming or renaming anything in a Unity project, even unasked: new class, field, prefab, material, sprite, animation clip, folder. Triggers: "what to call this", rename, naming convention, variant, numbered asset'
metadata:
  version: 1.3.2a0
---

## Unity Naming
One convention names every noun-type thing: class, member, variable, file, GameObject, folder.
- Casing: code per [Coder](#coder); asset file, folder, and GameObject in [Pascal Case](#letter-case-pascal-case)
- Characters: no spaces or punctuation but the underscore, per [Underscore Usage](#underscore-usage)
- Order: subject first, qualifier after, so related names sort together (`HeroIdle`, `HeroRun`, never `IdleHero`)
- Subject: name what a thing is or serves, omitting what its folder, per [Assets Management](#assets-management), already says (`Ball.prefab`, `Rock.mat`, `ButtonClick.mp3`)
- Suffix: end a name with its role when one in [Common Type and Suffix](#common-type-and-suffix) fits
- Numbers: zero-pad (`Explosion_02`, `Explosion_10`)
- File Match: a script file takes strictly its class's name (`PlayerManager.cs` holds `PlayerManager`)
- Imported: an external asset (art, download, DAW export) keeps its arrival filename, since others define it
- Dev: a dev-only asset or private copy takes `DEV`, an optional owner's name, then its name (`DEVSandboxScene.unity`, `DEVJohnMainScene.unity`)
#### Unit Usage
Suffix a numeric name holding a physical quantity with its unit, by this shorthand:
- deg:degree
- s:second
- u:world unit
- join units with `Per`, numerator first; a bare amount takes `Per` alone (`regenPerS`)
- apply to fields, locals, parameters, and getters (`MaxSpeedUPerS => maxSpeedUPerS`)
- leave a dimensionless value bare (ratio, count, multiplier), its range in the tooltip (`0~1`)
- end the field's tooltip with the same unit, per [Inspector Field](#inspector-field)
```csharp
[SerializeField]
[Tooltip("time stunned after a hit; s")]
private float hitStunDurationS = 0.4f;

[SerializeField]
[Tooltip("pull toward the anchor; u/s")]
private float pullSpeedUPerS = 3f;
```
#### Underscore Usage
The underscore carries these jobs, and no others:
- Key Prefix: a leading `_` sorts the key sibling first, a hub, base variant, or most used one, and takes no variant field (`_PopupBase.prefab`, `_Player.asset`)
- Variant or State: an inner `_` splits the subject from what tells one version of it apart, Pascal Case within each field (`Banana_Ripe.mat`, `Banana_Raw.mat`, `Player_Idle.anim`); use it whenever several things differ only by variant or state, such as two materials of one object, a sprite per state, or a prefab variant (`Popup_Confirm`, beside `_PopupBase`, per [Prefab Usage](#prefab-usage)); a further field may follow, such as a frame number or action (`Hero_Attack_01`)
- Channel: a texture map takes its channel as the variant field (`_Albedo`, `_Normal`), a packed map named for the channels it holds (`_MRA`)
### {[Claude:Skill] Usage}
If needed, invoke `coder`, `style-letter-case-pascal-case`, `u3d-assets-management`, `u3d-common-type-and-suffix`, `u3d-if`, or `u3d-pfb` skills via `Skill` tool.