# Trick Shot Constant Acceleration

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Trick Shot Constant Accelation has a 2D variant for use with Trick Shot 2D: `TrickShotConstantAcceleration` dynamically composes a 3D “gravity” (or any constant force) vector each frame by summing:

1. World‐space forces (e.g., gravity).
2. Local‐space forces (rotated by the GameObject’s current orientation).

It then assigns that combined acceleration to a sibling `TrickShot` component, ensuring your projectile always uses the correct constant acceleration—even if the launcher rotates or moves at runtime.

***

## Requirements

* This GameObject **must** have a **`TrickShot`** component (enforced by `[RequireComponent(typeof(TrickShot))]`).

***

## Public Fields

### Global Constants

* **`public List<Vector3> globalConstants`**
  * Forces expressed in **world‐space** (e.g., `(0, –9.81f, 0)` for earth‐gravity).
  * Defaults to one entry: `(0, –9.81f, 0)`.
  * Designers can add multiple entries here to combine several global forces (e.g., wind, custom gravity).

### Local Constants

* **`public List<Vector3> localConstants`**
  * Forces expressed in **local‐space**, relative to this GameObject’s transform.
  * Each entry is transformed by `transform.rotation` before being added.
  * Use this to apply forces that should follow the launcher’s orientation (e.g., a “downward” pull relative to a rotating turret).

***

## Usage Example

1. **Scene Setup**
   * Attach both **`TrickShot`** and **`TrickShotConstantAcceleration`** to your launcher GameObject.
2. **Inspector Configuration**
   * **`globalConstants`**
     * By default, `(0, –9.81f, 0)` is present.
     * To simulate a horizontal wind, add `(2f, 0, 0)`.
   * **`localConstants`**
     * To apply a downward pull relative to the turret—even if it tilts—add `(0, –9.81f, 0)` here.
3. **At Runtime**
   * Every frame, `TrickShotConstantAcceleration` calculates the sum of all listed vectors and writes it to `TrickShot.constantAcceleration`.
   * Your `TrickShot.Predict()` or `Shoot()` methods will then use this combined acceleration automatically.

***

## Designer Tips

* **Multiple Forces**
  * Combine wind, gravity, or any other constant fields by adding them to `globalConstants`.
  * For example, `(0, –9.81f, 0)` + `(1f, 0, 0)` applies both gravity and a constant rightward push.
* **Local vs. Global**
  * Use `localConstants` when the force should rotate with your GameObject (e.g., pulling “down” toward the launcher’s “bottom” even if it’s angled).
  * Forces in `localConstants` are transformed by `transform.rotation` each `LateUpdate`.
* **Overriding Static Values**
  * Any `constantAcceleration` value set directly on the `TrickShot` component will be overridden in `LateUpdate`.
  * If you need a fixed acceleration regardless of these lists, disable or remove this component.
* **Dynamic Adjustments**
  *   You can modify either list at runtime via script to change gravity or wind on the fly. Example:

      ```csharp
      csharpCopyEditvar accelHelper = GetComponent<TrickShotConstantAcceleration>();
      accelHelper.globalConstants.Add(new Vector3(0, 5f, 0)); // temporary upward thrust
      ```
