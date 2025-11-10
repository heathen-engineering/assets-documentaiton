# Ballistic Path Follow

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

`BallisticPathFollow` moves a GameObject along one or more precomputed ballistic paths (instances of `BallisticPath`). As it “plays” through each path segment, it:

* Steps the object’s position over time (using `FixedUpdate`/`LateUpdate`).
* Optionally validates any planned bounce‐impacts (so you don’t hit a surface that’s since moved).
* Optionally checks for unplanned collisions mid‐flight.
* Fires a UnityEvent (`endOfPath`) once the end of all path segments is reached (or a collision causes an early stop).
* Can re‐enable physics at the end (so your Rigidbody can resume dynamic movement).

Designers typically use this component when they have already generated a full flight path (via `BallisticPath.Get(...)`) and want an object (e.g., a projectile, grenade, or thrown item) to follow that path exactly, including triggering any collision callbacks at the right moment.

{% hint style="info" %}
BallisticPathFollow2D has the same funcitonlity simply in the 2D space.
{% endhint %}

### Demo Scene

You can see the Ballistic Path Follow and its 2D variant demonstrated in the (2D) and (3D) Deterministic Bounce Prediction scenes. Take a look at the projectile template in each scene and you will find the Ballistic Path Follow which is what causes the projectile to fallow the pre-planned path.

***

#### Public Fields (Designer-Facing)

* **`BallisticsData projectile`**\
  Reference to the projectile’s data (mass, radius, drag, etc.). Used internally for collision checks (e.g., sphere‐casting).
  * In the Inspector, you’ll see a slot for a `BallisticsData` ScriptableObject or component.
* **`List<BallisticPath> path`**\
  A list of precomputed ballistic trajectories (each a `BallisticPath`).
  * Assign as many segments as you like—for example, initial launch arc, then a bounce arc, etc.
  * Designers typically populate this list at runtime (e.g., right after calling `BallisticPath.Get(...)`).
  * If this list is empty or `null`, the component does nothing.
* **`bool resumeDynamicOnEnd`** (default: `true`)\
  If checked, once the entire `path` is complete (or stopped early by collision), the component finds the nearest parent `Rigidbody`, sets it to non-kinematic, and applies the final velocity so that Unity’s physics takes over naturally.

***

**Planned Collision Settings**

* **`bool validateBounce`** (default: `true`)\
  When following a `BallisticPath`, if a segment’s final sample contains an `impact` (i.e., where the physics cast expected to hit something), enabling this flag will re-test with a short, instantaneous `SphereCast` just before invoking the collision.
  * If the surface has moved or is gone, the component abandons the planned bounce and ends the path early.
  * If disabled, it will always invoke the planned collision regardless of whether the collider has shifted.
* **`bool invokeOnCollisionEnter`** (default: `true`)\
  If checked, at the moment the component reaches a segment’s planned impact, it enqueues an “artificial” `OnCollisionEnter` call on the target GameObject so that any scripts on that object with an `OnCollisionEnter(Collision)` callback will run.
  * Designers can disable this if they want to handle bounce logic entirely within custom scripts rather than rely on a simulated Unity collision.

***

**Unplanned Collision Settings**

* **`LayerMask collisionMask`** (default: `1` = “Default” layer)\
  Specifies which layers to test for unexpected collisions while following the path. If the projectile hits something outside of its planned path (e.g., you throw it near another object), the component can stop early.
  * Only used if **`endOnCollision`** is enabled.
* **`bool endOnCollision`** (default: `true`)\
  When checked, every `FixedUpdate` the component does a quick `Physics.SphereCast` from the object’s current position in the direction of its instantaneous velocity.
  * If it detects a collider on any of the layers in `collisionMask` that isn’t part of a planned impact, it stops the path immediately and triggers the same “end of path” logic (and event).

***

* **`Vector3Event endOfPath`**\
  A UnityEvent that fires when the path is finished or forcibly stopped by a collision.
  * The event’s payload is the final velocity (`float3`) of the object as it ends.
  *   Designers can hook any method (e.g., spawn an explosion, play a sound, enable a ragdoll) by assigning to this event in the Inspector or in code:

      ```csharp
      ballisticPathFollow.endOfPath.AddListener(finalVelocity => {
          // Your custom logic here
      });
      ```

***

#### Typical Designer Usage

1. **Scene Setup**
   * Attach `BallisticPathFollow` to the projectile prefab (or parent GameObject).
   * Ensure that the prefab either has a `Rigidbody` (set to “Kinematic” initially) or that a parent in the hierarchy has one.
2. **Compute & Assign Path**
   * In your firing script (e.g., when the player clicks “shoot”), call `BallisticPath.Get(...)` to get a `BallisticPath` for the initial launch.
   * If you expect bounces, compute subsequent segments by using the previous impact point/velocity as the new `start` and recomputing another `BallisticPath`.
   *   Assign all segments to the `path` list in `BallisticPathFollow`. Example:

       ```csharp
       // Suppose we already have a BallisticPath initialPath:
       var projectileFollow = projectileInstance.GetComponent<BallisticPathFollow>();
       projectileFollow.projectile = myBallisticsData;
       projectileFollow.path = new List<BallisticPath> { initialPath, bouncePath, finalPath };
       ```
3. **Configure Collision Behavior**
   * If you want to enforce “surface‐moved” detection on planned bounces, leave **`validateBounce`** = **`true`**.
   * If you want to skip simulating `OnCollisionEnter` (maybe you handle impacts in a different system), uncheck **`invokeOnCollisionEnter`**.
   * If you don’t need to stop for anything unexpected mid-flight (e.g., your scene is empty), uncheck **`endOnCollision`** to save needless checks.
   * To only collide with specific layers (e.g., “Environment” but not “Player Characters”), adjust **`collisionMask`** in the Inspector.
4.  **Hooking the End-of-Path Event**

    ```csharp
    projectileFollow.endOfPath.AddListener(finalVelocity => {
        // Example: switch on physics and let it fall naturally
        var rb = projectileInstance.GetComponent<Rigidbody>();
        rb.isKinematic = false;
        rb.velocity = finalVelocity;
        // (Or spawn an explosion, play sound, etc.)
    });
    ```
5. **Runtime Behavior**
   * As soon as the GameObject is enabled (or when `path` is non-empty), `BallisticPathFollow` begins simulating motion.
   * Each `LateUpdate`, it calculates how far along the concatenated `path` list it should be (based on `Time.time - startTime`).
   * If it reaches a planned impact point:
     * It optionally re-validates whether that surface still exists.
     * It enqueues an artificial `OnCollisionEnter` on the impacted GameObject (so any scripts there respond as if hit by a real Unity collision).
     * If the bounce is invalid (surface moved), it stops early.
   * If it detects an unplanned sphere‐cast hit (and `endOnCollision` is enabled), it stops immediately.
   * When it finally cannot advance any further (all segments done or a collision forced stop):
     * If **`resumeDynamicOnEnd`** is true, it flips the nearest parent `Rigidbody` back to non-kinematic and sets its velocity so Unity physics takes over.
     * Fires the **`endOfPath`** UnityEvent with the ending velocity (or zero if it never moved).

***

#### Designer Tips

*   **Preparing Multiple Segments**\
    If you expect your projectile to bounce (e.g., off a wall or the ground), compute each segment in sequence and add them to the `path` list. For example:

    ```csharp
    // 1. First segment: from muzzle to first bounce:
    BallisticPath first = BallisticPath.Get(startPos, startCollider, launchVelocity, radius, resolution, maxLen, layerMask);
    if (first.impact.HasValue)
    {
        // 2. Compute bounce velocity via reflection off the first impact’s normal:
        Vector3 bounceVel = Vector3.Reflect(first.steps[^1].velocity, first.impact.Value.normal);
        // 3. Second segment: from impact point, using bounceVel:
        BallisticPath second = BallisticPath.Get(first.impact.Value.point, /* same collider? */ collider, bounceVel, radius, resolution, maxLen, layerMask);
        projectileFollow.path = new List<BallisticPath> { first, second };
    }
    else
    {
        projectileFollow.path = new List<BallisticPath> { first };
    }
    ```
* **Skipping Event Injection**\
  By default, `BallisticPathFollow` finds any `OnCollisionEnter(Collision)` methods on the impacted GameObject and invokes them via reflection. If your gameplay already handles bounce logic entirely within a different event (e.g., you manually spawn a decal or sound when the path ends), uncheck **`invokeOnCollisionEnter`** and listen only to `endOfPath`.
* **Collision Layers**
  * **Planned impacts** always use whatever layers you originally sampled when calling `BallisticPath.Get(...)`.
  * **Unplanned impacts** use the `collisionMask`. Make sure your projectile’s own collider (or parent colliders) is excluded so it doesn’t immediately collide with itself.
* **Pausing or Resuming**
  * If you disable the GameObject mid-flight (e.g., pausing the level), `LateUpdate` stops advancing. Upon re-`OnEnable`, it resets `time = Time.time` so it will continue where it left off.
  * To reset entirely, clear or replace `path` and toggle the component off/on.

***

By assigning a precomputed list of `BallisticPath` segments and configuring the collision flags, designers can have a projectile follow exactly the path they planned—complete with bounces, bounce validation, automatic invocation of any impacted object’s `OnCollisionEnter`, and the option to hand control back to Unity’s physics at the end.
