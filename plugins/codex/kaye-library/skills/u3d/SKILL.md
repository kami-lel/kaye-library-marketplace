---
name: u3d
description: Sets baseline for all Unity 6 C# work, the shared root every topic-specific Unity skill builds on
when_to_use: 'Any C# in a Unity project, even when user never says "Unity": gameplay, managers, editor tools, UI, save/load. Triggers: Unity, `UnityEngine`, `.cs` under `Assets/`, `MonoBehaviour`, `ScriptableObject`'
metadata:
  version: 1.6.2
paths:
- '**/*.cs'
---

## Brace Style
- opening `{` on the **same line** as the declaration
- closing `}` on its **own line**
## Coder C Sharp
Writing code based on [Coder](#coder)
Documentation: Use XML comments (`/// <summary>...</summary>`) to document functionality and provide examples wherever helpful.
# Unity Engine
Follows [Coder C Sharp](#coder-c-sharp)
Writing code based on [Coder](#coder)
Decode-only, never output the shorthand:
- pfb:Prefab
- edr:Unity Editor
- acv:activate
- C:child (object)
- collr:collider
- colln:collision
- cpn:component
- dcv:deactivate
- hrcy:hierarchy
- IF:inspector field
- P:parent (object)
- xfm:transform
- trg:trigger
When naming an identifier, always use shorthand below over full word; decode any user writes:
- GO:GameObject
- Mat:Material
- MB:MonoBehavior
- Rb:Rigidbody
- SO:ScriptableObject
- efx:effect
- Lv:level
- SFX:sound effects
- VFX:visual effects
Unity conventions:
- name code & assets per [Unity Naming](#unity-naming)
- pick a class role from [Common Type and Suffix](#common-type-and-suffix)
- write C# logic per [Unity Coding](#unity-coding)
  - expose fields per [Inspector Field](#inspector-field)
  - lay out a component per [MonoBehaviour](#monobehaviour)
  - lay out a data asset per [Scriptable Object](#scriptable-object)
- place assets & folders per [Assets Management](#assets-management)
- build prefabs & variants per [Prefab Usage](#prefab-usage)
- show & hide objects mid-run per [Owner-Driven Activation](#owner-driven-activation)
- move tuning values into data per [Game Tuning](#game-tuning)