---
name: u3d-pfb
description: Turns Unity scene objects into prefabs & variant families early, so one edit updates every copy
when_to_use: 'Building, duplicating, or reviewing scene objects, even when user never says "prefab": copy-pasted GameObjects, a 2nd enemy type, reusable popup, near-identical variants. Triggers: prefab, Prefab Variant, duplicate, reuse, "same as that one but"'
metadata:
  version: 1.6.2
---

## Prefab Usage
Reach for prefabs extensively: turn an object into a prefab as soon as a reason below holds, progressively as the project grows, rather than waiting for a cleanup pass. Store each under `Prefabs/` per [Assets Management](#assets-management).
Make a prefab when:
- 2 or more objects are copies or variants of each other
- the object could be reused elsewhere, such as in another scene, even if it is used once today
Prefer the base and variant pattern for a family of near-identical objects:
- base prefab: holds everything the family shares, named with a leading `_`, the subject, and `Base` (`_PopupBase.prefab`)
- variant prefab: a Prefab Variant of the base, overriding only what differs, named per [Underscore Usage](#underscore-usage) (`Popup_Confirm.prefab`)
- put a change shared by the whole family in the base, so every variant follows it
- a scene holds instances of the prefab, never a hand-made copy of one
### {[Claude:Skill] Usage}
If needed, invoke `u3d-assets-management` or `u3d-naming` skills via `Skill` tool.