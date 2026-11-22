---
name: u3d-common-type-and-suffix
description: Assigns each Unity class, script, GameObject, or asset one architectural role, so responsibilities split cleanly & its name says what it does
when_to_use: 'Designing a Unity system or deciding what a new class should own, even when user only asks "manager or controller?": splitting a god class, picking a pattern, reviewing a misnamed script. Triggers: manager, controller, architecture, responsibility, design pattern, MVP, event pipe, "what should this class be"'
metadata:
  version: 1.5.1
---

## Common Type and Suffix
Each type names a concept, not a script: give its suffix to whatever embodies that concept, be it a class, script or asset file, GameObject, prefab, or variable, its full name spelled per [Unity Naming](#unity-naming).
Scene Behaviour:
- Controller: drives one subject frame by frame, turning input or state into actions (`PlayerController`, `GameController`)
- Manager: owns one system's state for the whole run, exposing an API over it, never running a multi-step flow (`AccessoryManager`)
- Coordinator: runs one multi-step flow across several systems, in order (`LevelTransitionCoordinator`)
- Director: plays one authored timeline, firing content at scripted moments (`WaveDirector`)
- Spawner: decides where and when instances enter the scene, leaving construction to a Factory (`EnemySpawner`)
Entity Behaviour:
- Motor: turns a wanted direction or speed into velocity or force on one body (`CharacterMotor`)
- Sensor: detects what surrounds one entity and reports it, deciding nothing (`VisionSensor`)
- Ability: one activatable action of a character, with its own trigger, cost, and cooldown (`DashAbility`)
- Command: one action made an object, so it can be queued, replayed, or undone (`MoveCommand`)
- State: the behaviour of one state machine node (`PatrolState`)
- StateMachine: owns one entity's states and the transitions between them (`EnemyStateMachine`)
- Feedback: one burst of particles, sound, or camera shake, played on request (`HitFeedback`)
Event Delivery:
- Relay: passes one object's trigger or event callbacks on to an owner, holding no response logic (`DetectionZoneRelay`)
- Channel: one event pipe, so raiser and listener never reference each other (`GameOverEventChannel`)
Event Reaction:
- Listener: subscribes to one event source, a channel or a subject's event, and reacts on its own object (`PauseListener`)
- Binder: mirrors every state change of one known subject into its own object (`HealthBinder`)
World Object:
- Pickup: one collectible, handing its reward over once on touch (`BananaPickup`)
- Projectile: one thrown or fired thing, flying until it hits or expires (`CoconutProjectile`)
- Zone: one volume applying an effect to whatever is inside it (`SlowZone`)
Object Supply:
- Factory: creates and configures new instances of one type, hiding how (`EnemyFactory`)
- Pool: lends and reclaims reusable instances of one prefab, instead of instantiate and destroy (`BulletPool`)
- Registry: tracks live instances of one type, which register themselves, for lookup and iteration (`EnemyRegistry`)
- Generator: produces procedural content from rules and a seed (`LevelGenerator`)
- Provider: hands out one value or dependency on request, without owning its lifecycle (`InputProvider`)
- Service: logic behind an interface, with no scene presence and little or no state (`SaveService`)
- Loader: brings assets or scenes into memory, usually asynchronously (`SceneLoader`)
User Interface, shown & hidden per [Owner-Driven Activation](#owner-driven-activation):
- Screen: one full-screen interface, opening, closing, and owning its panels (`PauseScreen`)
- Panel: one self-contained region of a screen (`InventoryPanel`)
- Popup: a modal prompt shown over the current screen, then dismissed (`ConfirmPopup`)
- Toast: a timed, non-modal message shown over play, fading on its own, never blocking input (`HintToast`)
- Widget: a small reusable control with its own look and behaviour (`HealthBarWidget`)
MVP:
- Model: one feature's data and rules, ignorant of any display, raising events on change (`InventoryModel`)
- View: a passive display deciding nothing, exposing what to show and which input occurred (`InventoryView`); without a Presenter, use Panel or Widget
- Presenter: links one Model to one View, so neither knows the other (`InventoryPresenter`)
Authored Data, chosen per [Game Tuning](#game-tuning), shaped per [Scriptable Object](#scriptable-object):
- Config: tunable values, read by whatever it configures (`AudioConfig`)
- Definition: the authored content of one thing, read-only at runtime (`WeaponDefinition`)
- Setting: options the player or project chooses, apart from a Config's designer tuning (`GraphicsSetting`)
- Catalog: every Definition of one kind, collected for lookup by id (`ItemCatalog`)
- Preset: named values bundled to apply in one step (`DifficultyPreset`)
- Save: a record of progress, persisted to disk (`PlayerSave`)
### {[Claude:Skill] Usage}
If needed, invoke `u3d-naming`, `u3d-owner-driven-activation`, `u3d-game-tuning`, or `u3d-so` skills via `Skill` tool.