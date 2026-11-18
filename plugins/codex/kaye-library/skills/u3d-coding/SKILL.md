---
name: u3d-coding
description: Writes, edits & reviews Unity C# logic in house idiom, so code reads consistently & a debug session traces as a sequence of events
when_to_use: 'Writing or reviewing any Unity C# behaviour, even when user only asks for a feature: game logic, input handling, events, singletons, debug output. Triggers: `Debug.Log`, `InputAction`, singleton, event, "add logging", "read input"'
metadata:
  version: 1.5.0
---

## Brace Style
- opening `{` on the **same line** as the declaration
- closing `}` on its **own line**
## Coder C Sharp
Writing code based on [Coder](#coder)
Documentation: Use XML comments (`/// <summary>...</summary>`) to document functionality and provide examples wherever helpful.
## Unity Coding
- `var` only for a `foreach` local or a long generic right-hand side
- singleton: expose the instance through a static member named exactly `I` (`GamepadManager.I`)
- events: prefer the C# `event` keyword over `UnityEvent` (`public event Action<int> HealthChanged;`)
- member order in a plain class: `[SerializeField]` fields, public API, plain fields, private helpers, constructor last; a `MonoBehaviour` follows [MonoBehaviour](#monobehaviour), a `ScriptableObject` [Scriptable Object](#scriptable-object)
- serialized fields: declare per [Inspector Field](#inspector-field)
- gameplay numbers: keep in data per [Game Tuning](#game-tuning), never as literals
- banners per [Comment Banner](#comment-banner), laid out as the example shows, and none at all in a small or single-purpose file
- name every class, member, and variable per [Unity Naming](#unity-naming), suffixed per [Common Type and Suffix](#common-type-and-suffix) and [Unit Usage](#unit-usage)
#### Input
Read gameplay input through the Input System: `InputAction`s from an Input Actions asset, kept in `Inputs/` per [Assets Management](#assets-management), never a keyboard, mouse, or gamepad directly. Express timing, such as a double-tap, as an interaction (`MultiTap`), never as a hand-rolled key tracker
#### Logging
Log every meaningful state change so a debug session reads as a sequence of events: lifecycle transitions, branch decisions, external calls (network, save/load, scene loads).
Open every message with the owning subsystem or module name, a colon, and a tab.
Warning and error are reserved for a failed guard clause, such as the Inspector Assignment Guard in [MonoBehaviour](#monobehaviour). Every other log is debug level, gated by `Debug.isDebugBuild` and braced even for one statement.
```csharp
private void Awake() {
    if (rb == null) {
        Debug.LogError("Inventory:\tfail to get Component: Rigidbody2D", this);
    }
    if (itemPrefab == null) {
        Debug.LogWarning(
            "Inventory:\tmust assign Inspector Field: Item Prefab", this);
    }
    if (Debug.isDebugBuild) {
        Debug.Log("Inventory:\tready");
    }
}
```