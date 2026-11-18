---
name: u3d-if
description: Declares Unity Inspector fields so designers read, tune & rename them without breaking saved values
when_to_use: 'Adding, renaming, or reviewing any value exposed in the Inspector, even when user only says "expose this" or "make it tweakable". Triggers: `[SerializeField]`, Inspector, public field, "show in editor", tooltip'
metadata:
  version: 1.5.0
---

### Inspector Field
Applies to every serialized field of a [MonoBehaviour](#monobehaviour) or [Scriptable Object](#scriptable-object), each named per [Unity Naming](#unity-naming).
- declare as `[SerializeField] private`, never a public field
- prefer `[Tooltip]` on each field, worded in briefness style, ending with its unit per [Unit Usage](#unit-usage)
- prefer `[Header]` dividing fields into groups
- put a simple numeric bound in `[Min]` or `[Range]`; `OnValidate` only for a rule they cannot state
- add `[RequireComponent]` on a class that reads a sibling component
- add `[FormerlySerializedAs]` on a renamed field, keeping its saved values
```csharp
[RequireComponent(typeof(Rigidbody2D))]
public class CharacterMotor: MonoBehaviour {
    [Header("Movement")]
    [SerializeField]
    [Tooltip("top speed; u/s")]
    [Min(0f)]
    private float maxSpeedUPerS = 5f;

    [SerializeField]
    [FormerlySerializedAs("jumpPower")]
    [Tooltip("launch speed of a jump; u/s")]
    private float jumpSpeedUPerS = 8f;
}
```