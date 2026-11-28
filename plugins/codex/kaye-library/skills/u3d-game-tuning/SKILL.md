---
name: u3d-game-tuning
description: Moves Unity gameplay numbers out of code into designer-editable data, so balance changes need no recompile
when_to_use: 'Any tunable gameplay value, even unasked: speed, damage, cooldown, spawn rate, difficulty ramp, hard-coded magic number. Triggers: balance, tuning, difficulty, curve, "let the designer tweak", magic number'
metadata:
  version: 1.6.2
---

## Game Tuning
Prefer tunable gameplay numbers in data over code (speed, damage, cooldown, spawn rate, ramp): a designer can then adjust them in the Inspector, even in Play mode, without a recompile. A structural constant (a tag, a layer, an array size) is not tuning, and a `const` suits it.
Tuning leans on three objects, each per its [Common Type and Suffix](#common-type-and-suffix) role, each class shaped per [Scriptable Object](#scriptable-object):
- Config: SO holding the tuning values of one concern, the core structure of tuning (`PlayerBalanceConfig`)
- Definition: SO holding what one thing is, its identity and own stats, one asset per thing (`WeaponDefinition`)
- Preset: bundle of named values applied to a Config in one step, eg a difficulty tier (`DifficultyPreset`)
Config vs Definition: a Config answers how a system behaves, a Definition answers what a thing is. A value shared by every instance of a system tends to suit a Config; a value that differs per thing tends to suit its Definition.
Config leanings:
- one Config per concern, with balance split into a few assets (player, world, enemy) rather than one asset for everything or one asset per field
- a reader holds a `[SerializeField]` for the one Config it needs, rather than a hub asset reaching every concern
- treat a Config as read-only at runtime: a reader can copy a value into its own state before changing it, since an edit made in Play mode would persist in the asset
- expose each private serialized field as a read-only `=>` getter
- clamp in `OnValidate` under an `// Editor Validation` banner, so an out-of-range value does not reach play
- let one reader own the meaning of each value; a second reader of the same value can ask the Config instead of keeping its own copy
- let a Preset overwrite Config values through its single apply entry point rather than from scattered code
#### Tuning with AnimationCurve
Reach for an `AnimationCurve` extensively when a value depends on another value, in place of a formula or a table of constants: difficulty ramping, falloff by distance, damage by charge, speed by health fraction, reward by streak. The designer draws the curve, so its shape can change without code.
Common x axes:
- elapsed time of a run or an encounter
- difficulty level or wave number
- normalized progress, 0~1
- distance, health fraction, stack count
Preferences:
- name the field `<Value>Curve` and state both axes with units per [Unit Usage](#unit-usage) in its `[Tooltip]`, x first (`x: ramp progress 0~1; y: spawn interval; s`)
- normalize x to 0~1 when its range varies, and keep the range in a separate Config field (a ramp duration), so one curve serves any length
- hide `Evaluate` behind a Config method that clamps x (`GetIntervalS(elapsedS)`), so a reader need not touch the curve
- give a curve a non-empty initializer (`AnimationCurve.Linear`), since an unset curve evaluates to 0 and silently zeroes the value
- let the y axis be a multiplier on a base value when one curve shapes several values, and absolute when it shapes one
- a plain float still suits a value that depends on nothing
```csharp
[CreateAssetMenu(menuName = "Scriptable Objects/SpawnBalanceConfig")]
public class SpawnBalanceConfig: ScriptableObject {
    // Public Members  #########################################################
    public float GetIntervalS(float elapsedS) =>
        intervalCurve.Evaluate(Mathf.Clamp01(elapsedS / rampDurationS));

    // Inspector Fields  #######################################################
    ~~~
}
```