# Ballistics Aim

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Ballistic Aim 2D has the same funcitonality and is simply limited to 2D space.
{% endhint %}

`BallisticAim` is a MonoBehaviour that computes and applies the required yaw (Y-axis) and pitch (X-axis) rotations for a two-pivot launcher (e.g., turret or cannon) to hit a specified 3D target. It leverages the core `Ballistics.Solution` methods to solve for projectile trajectories, taking into account an initial muzzle speed and constant acceleration (gravity). The component enforces configurable rotational limits on both pivots, returning whether the calculated aim falls within those limits.

### Demo Scene

See the (32) Targeting Tool scene for a practical demonstration of the tool.

***

### Namespace & Dependencies

```csharp
using Heathen.UnityPhysics.API;    // Provides Ballistics.Solution(...)
using Unity.Mathematics;           // For math.clamp and related utilities
using UnityEngine;
using UnityEngine.Serialization;    // For [FormerlySerializedAs]
```

***

## Fields & Properties

### initial Speed The muzzle (launch) speed of the projectile in units/second.

* Displayed in the Inspector as “Initial Speed” (formerly named `initialVelocity`).

### **Constant Acceleration**

The acceleration vector applied to the projectile throughout its flight (typically gravity).

* Default value: `(0, –9.81f, 0)`.

### **Y Pivot**

Reference to the yaw pivot (parent pivot) around which horizontal rotation is applied.

* Expected to rotate about its local Y-axis.

### **X Pivot**

Reference to the pitch pivot (child of `yPivot`) that tilts up/down.

* Expected to rotate about its local X-axis.

### **Y Limit**

Minimum/maximum allowed yaw angles (in degrees) relative to world-space zero.

* Default: `(-180, 180)`.

### **X Limit**

Minimum/maximum allowed pitch angles (in degrees) relative to local zero.

* Default: `(-180, 180)`.

***

## Public Methods

### Aim(Vector3 target)

Calculates a firing solution for a stationary target.

1.  Calls

    ```csharp
    Ballistics.Solution(yPivot.position,
                        initialSpeed,
                        target,
                        constantAcceleration,
                        out Quaternion lowAngle,
                        out _);
    ```

    * If the returned solution count is ≤ 0, the method returns `false` (no valid trajectory).
    * Otherwise, it applies `lowAngle` to the two pivots (Y-pivot then X-pivot) via `ApplyAimRotation(...)` and returns whether both yaw and pitch remain within their specified limits.

### Aim(Vector3 target, Vector3 targetVelocity)

Calculates a firing solution for a moving target.

1.  Calls

    ```csharp
    Ballistics.Solution(yPivot.position,
                        initialSpeed,
                        target,
                        targetVelocity,
                        constantAcceleration.magnitude,
                        out Quaternion lowAngle,
                        out _);
    ```

    * This overload factors in linear target motion (leading).
    * If no valid solution exists, returns `false`; otherwise, applies `lowAngle` and returns whether the resulting angles respect `yLimit` and `xLimit`.

***

## Usage Example

1. **Scene Setup**
   * Create an empty GameObject named “TurretRoot” (this is the `yPivot`).
   * As a child of “TurretRoot”, create “TurretBarrel” (this is the `xPivot`).
   * Attach your projectile-spawning script as a child of “TurretBarrel” so its forward (local Z+) direction is the launch direction.
   * Add the `BallisticAim` component to “TurretRoot”.
2. **Inspector Assignment**
   * Drag “TurretRoot” into the `yPivot` slot.
   * Drag “TurretBarrel” into the `xPivot` slot.
   * Set **Initial Speed** to your muzzle velocity (e.g., `50f`).
   * Leave **Constant Acceleration** at `(0, –9.81f, 0)` for Earth-like gravity.
   * Adjust **Y Limit** and **X Limit** to prevent over-rotation or self-collision (e.g., `yLimit = (–90, +90)`, `xLimit = (–5, +45)`).
3.  **Runtime Aim Call**

    ```csharp
    public class TurretController : MonoBehaviour
    {
        [SerializeField] private BallisticAim ballisticAim;
        [SerializeField] private Transform target;

        void Update()
        {
            Vector3 targetPosition = target.position;
            // Optionally, if the target moves:
            Vector3 targetVelocity = target.GetComponent<Rigidbody>()?.velocity ?? Vector3.zero;

            // Try to aim; if false, no valid shot or out of limits
            bool canAim = ballisticAim.Aim(targetPosition, targetVelocity);
            // You might highlight UI or disable firing if canAim == false
        }
    }
    ```

***

## Behavior Notes

* **Low-Angle Solution**: This component always uses the “low” solution returned by `Ballistics.Solution`. If you’d prefer a high-arc trajectory, replace `lowAngle` with the `highAngle` output instead.
* **Limit Enforcement**: If the yaw or pitch is outside the configured ranges, the angle is clamped and the method returns `false`. You can detect out-of-bounds by checking the return value.
* **Pivot Hierarchy**: It is crucial that `xPivot` be a direct child of `yPivot`. Otherwise, local pitch rotations will not behave correctly relative to yaw.
