---
name: u3d-mb
description: Structures Unity `MonoBehaviour` scripts in one fixed layout, so every component reads alike & missing Inspector assignments surface at startup
when_to_use: 'Any Unity script attached to a GameObject, the default shape of most gameplay code, even when user never names `MonoBehaviour`: player, enemy, trigger zone, camera rig, UI behaviour. Triggers: `MonoBehaviour`, `Awake`, `Update`, `OnTriggerEnter`, `GetComponent`, "add a component"'
metadata:
  version: 1.5.0
---

## Style Guide Briefness Style
- write in **newspaper headlinese**, prioritize brevity over grammar
- use present for current, infinitive for planned
- omit articles (a, an, the) and helper verbs, use strong nouns, verbs
- compress with punctuation: colon, dash, comma, otherwise minimize, no terminal periods
- use numerals (use 2, not two), symbols, common abbreviations when unambiguous
- prefer active voice
- keep sentences short, direct, drop filler
Aggressively replace the full form with its shorthand:
- vs.:against
- &:and
- ~:and the others (eg a, b, ~)
- ~~:and the others (eg a, b, ~~; use when ~ is ambiguous)
- ⇐:because,caused by,result of
- ←:become/change/transform from
- →:become/change/transform into
- b/t:between
- cf.:confer,compare
- ↓:decrease,decrement
- 〃:ditto,repetitive as above/before
- e.g.:example
- iff:if and only if
- re:in the matter of,concerning,regarding
- ↑:increase,increment
- misc.:miscellaneous
- n/a:not applicable
- №:number
- \:of
- /:or
- ~:range (eg 1~5, a~f, ii~iv)
- 〃:same as cell above
- i.e.:that is,in other words
- ⇒:therefore,causing,resulting
- ※:which see,reference to
- w/:with
- w/i:within
- w/o:without
### MonoBehaviour
Section order, formatting, and accessors follow the example exactly.
Name the class and its members per [Unity Naming](#unity-naming), its role suffix per [Common Type and Suffix](#common-type-and-suffix); declare fields per [Inspector Field](#inspector-field); toggle a short-lived object per [Owner-Driven Activation](#owner-driven-activation).
Inspector Assignment Guard:
- guard **every** `[SerializeField] private` field carrying no declaration default (`private string label = "default";` needs none)
- **one block, at the top** of `Awake()`, under exactly one `// Inspector Assignment Guard` line, never scattered, never repeated
- word each failed guard per [Logging](#logging)
```csharp
public class PlayerController: MonoBehaviour {
    // Public Members  #########################################################
    public GameState currentState;

    // Public Methods  #########################################################
    public static PlayerController FindInScene() { ... }

    // Inspector Fields  #######################################################
    ~~~

    // MonoBehaviour Lifecycle  ################################################
    private void Awake() {
        // Inspector Assignment Guard  -----------------------------------------
        if (nextSceneName == null) {
            Debug.LogWarning(
                "MinigameRacing:\tmust assign Inspector Field: nextSceneName",
                this);
        }
        ...  // other guards, then other code
    }
    private void Start() { ... }

    // Event Handlers  #########################################################
    private void OnSceneLoaded(Scene scene, LoadSceneMode mode) { ... }

    // constants  ##############################################################
    private const string LOAD_TRIGGER_TAG = "LoadNextSceneTrigger";

    // private members  ########################################################
    private float startVelocityX;

    // cached references  ------------------------------------------------------
    private Rigidbody2D body;

    // private methods  ########################################################
    private void PlayIntroSequence() { ... }
}
```