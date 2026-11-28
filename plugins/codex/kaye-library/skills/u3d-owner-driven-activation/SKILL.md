---
name: u3d-owner-driven-activation
description: Controls Unity GameObjects living only part of a run through one owner, so showing, hiding & spawning stay predictable & cost nothing while idle
when_to_use: 'Showing, hiding, spawning, or enabling objects mid-run, even when user only says "open the menu" or "turn it on": pause screen, popup, toast, pooled enemy, cutscene prop. Triggers: `SetActive`, show/hide, enable/disable, toggle, "appear when"'
metadata:
  version: 1.6.2
---

## Owner-Driven Activation
Save a GameObject inactive when it lives for only a stretch of the run; let an owner, such as a Screen, Coordinator, or Pool per [Common Type and Suffix](#common-type-and-suffix), call `SetActive`, with no `Update` flag guards
Apply to:
- UI: pause screen, game over screen, settings panel, tutorial overlay, popup, toast, tooltip
- spawned or pooled: enemy, projectile, pickup, hit flash, particle effect, decal
- scripted: cutscene prop, event actor, boss arena gate, tutorial arrow
- mode-specific: alternate camera, debug panel, editor-only stand-in
- streamed: level section loaded in and out by distance or progress
Don't apply to:
- manager, singleton, event hub, listener
- camera follow, input reader, audio mixer
- the owner itself
Rules:
- hold each target in a `[SerializeField]` reference on the owner, declared per [Inspector Field](#inspector-field), never find it by search
- subscribe and reset in `OnEnable`, unsubscribe in `OnDisable`
- give each target one entry point (`Show`, `Hide`), and call only that from the owner
- assign each toggled group exactly one owner
- rest each object in its original active state: a screen is saved inactive and switched on by its owner, a manager is saved active and stays so
- toggle component `enabled`, a child visual, or `CanvasGroup` instead when the object must stay findable or listening
- play a hide state before `SetActive(false)` when the object needs an exit animation