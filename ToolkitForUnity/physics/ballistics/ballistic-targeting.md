# Ballistic Targeting

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

`BallisticTargeting` is a lightweight helper that sits on a GameObject with a `BallisticAim` component. Every frame (in `LateUpdate`), it attempts to aim at a designated `targetTransform`. It exposes a read‐only `HasSolution` flag indicating whether a valid ballistic solution exists for the current target position. Designers can swap targets at runtime via `SetTarget(...)`.

***

## Requirements

* The GameObject must have a **`BallisticAim`** component (enforced by `[RequireComponent(typeof(BallisticAim))]`).

***

## Public Fields

* **`public Transform targetTransform`**
  * Drag a Transform (e.g., an enemy, waypoint, or moving object) into this slot via the Inspector.
  * The component will attempt to calculate a low‐arc solution to this position every frame.

***

## Public Properties

* **`public bool HasSolution { get; private set; }`**
  * **Read‐only** property that returns **`true`** if the most recent call to `ballisticAim.Aim(...)` succeeded (i.e., a valid firing angle exists to hit `targetTransform.position`).
  * If `targetTransform` is unset (`null`) or out of range, `HasSolution` becomes **`false`**.

***

## Public Methods

* **`public void SetTarget(Transform newTarget)`**
  * Assigns a new `Transform` to `targetTransform`.
  * Can be called from other scripts to change who or what this turret should aim at.
  *   Example:

      ```csharp
      csharpCopyEditvoid SwitchEnemy(Transform nextEnemy)
      {
          GetComponent<BallisticTargeting>().SetTarget(nextEnemy);
      }
      ```

***

## Usage Example

1. **Scene Setup**
   * Attach both **`BallisticAim`** and **`BallisticTargeting`** to your turret (or launcher) GameObject.
   * Assign the turret’s Y‐pivot and X‐pivot inside the `BallisticAim` component.
   * In `BallisticTargeting`, drag the enemy’s Transform (e.g., “Enemy1”) into `targetTransform`.
2.  **Runtime Behavior**

    ```csharp
    csharpCopyEditpublic class TurretController : MonoBehaviour
    {
        private BallisticTargeting targeting;

        void Awake()
        {
            targeting = GetComponent<BallisticTargeting>();
        }

        void Update()
        {
            if (targeting.HasSolution)
            {
                // We have a valid firing solution—enable shooter, show reticle, etc.
            }
            else
            {
                // Out of range or no target—disable fire button or show “no lock”
            }
        }

        public void ChangeTarget(Transform newEnemy)
        {
            targeting.SetTarget(newEnemy);
        }
    }
    ```

    * Each frame, `BallisticTargeting` calls `ballisticAim.Aim(targetTransform.position)` internally.
    * `HasSolution` updates automatically, so your UI or firing logic can react immediately.

***

## Designer Tips

* **Unassigned Target**
  * If `targetTransform` is left **`null`**, `HasSolution` will always be **`false`** and the turret won’t rotate. This is useful for “idle” states where you don’t want the turret to seek anything.
* **Target Swapping**
  * Call `SetTarget(...)` from other gameplay scripts (e.g., when switching between multiple enemies).
  * If you need a “clear target” behavior, call `SetTarget(null)` to reset.
* **Checking `HasSolution`**
  * Use `HasSolution` in your HUD to display a “lock‐on” reticle only when a shot is possible.
  * Poll it in `Update()` to toggle the “Can Fire” icon or disable the fire button if no solution exists.
* **Combining with `BallisticAim` Settings**
  * Ensure that `initialSpeed`, `constantAcceleration`, and pivot limits in `BallisticAim` are configured so that targets you want to hit lie within range. Otherwise, `HasSolution` will be **`false`** for unreachable positions.
