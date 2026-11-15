---
name: u3d-so
description: Structures Unity `ScriptableObject` classes in one fixed layout, keeping asset data read-only & valid at runtime
when_to_use: 'Any designer-editable data living outside a scene, even when user only says "config", "settings", "database", "shared data": level config, item stats, event channel. Triggers: `ScriptableObject`, `CreateAssetMenu`, `.asset`, data container'
metadata:
  version: 1.3.2a0
---

### Scriptable Object
Section order, formatting, and accessors follow the example exactly.
Name the class per [Unity Naming](#unity-naming), its role suffix per [Common Type and Suffix](#common-type-and-suffix); declare fields per [Inspector Field](#inspector-field); decide which values it holds per [Game Tuning](#game-tuning).
Menu Path:
- one `[CreateAssetMenu]` per class, `menuName` always `"Scriptable Objects/<ClassName>"`
Data Access:
- every serialized field is `private`, exposed through a read-only `=>` getter under Public Members, documented with `<returns>`
- no public mutable field and no setter: asset data is read-only at runtime, since an edit made in Play mode would persist in the asset
Editor Validation:
- `OnValidate` sits last under an `// Editor Validation` banner, keeping a rule an attribute cannot state (a cross-field bound)
- no `Awake` and no Inspector Assignment Guard: a Config's fields all carry declaration defaults
```csharp
[CreateAssetMenu(menuName = "Scriptable Objects/PlayerBalanceConfig")]
public class PlayerBalanceConfig: ScriptableObject {
    // Public Members  #########################################################
    /// <returns>slowest allowed speed; u/s</returns>
    public float MinSpeedUPerS => minSpeedUPerS;
    /// <returns>top speed; u/s</returns>
    public float MaxSpeedUPerS => maxSpeedUPerS;

    // Inspector Fields  #######################################################
    ~~~

    // Editor Validation  ######################################################
    private void OnValidate() {
        maxSpeedUPerS = Mathf.Max(minSpeedUPerS, maxSpeedUPerS);
    }
}
```