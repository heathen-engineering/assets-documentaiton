# Ballistic Path

A struct used in several of our tools: `BallisticPath` represents the full flight trajectory of a projectile in Unity, sampling its position, velocity, and elapsed time at discrete “steps.” It also records its total flight distance and time, plus any collision (`impact`) detected along the way. Designers and gameplay programmers can use it to preview trajectories, visualize flight arcs, or query where/when a projectile will be at any given moment.

{% hint style="info" %}
BallisticPath2D is the same functionality for tools in the 2D space.
{% endhint %}

***

## Public Fields

* **`(Vector3 position, Vector3 velocity, float time)[] steps`**\
  An ordered array of tuples, each containing:
  1. **`position`** – World‐space position of the projectile at that sample.
  2. **`velocity`** – World‐space velocity vector at that sample.
  3. **`time`** – Elapsed time (since launch) when the sample was recorded.
  4. Use this array to iterate through the sampled trajectory for drawing gizmos, spawning effects, or debugging.
* **`float flightDistance`**\
  The cumulative distance (in world units) traveled by the projectile along its path, up until impact or until it reached its maximum tracing length.
* **`float flightTime`**\
  The total time (in seconds) from launch until the projectile either collides or reaches the end of its traced path.
* **`RaycastHit? impact`**\
  A nullable `RaycastHit` struct describing the collision point, normal, collider reference, etc.
  * If `impact` is `null`, no collision occurred within the specified max length.
  * If non‐null, you can read `impact.Value.point`, `impact.Value.normal`, `impact.Value.collider`, and so on.

***

## Static Properties

* **`static BallisticPath Empty`**\
  Returns a `BallisticPath` with:
  * `steps` = an empty array
  * `flightDistance` = 0
  * `flightTime` = 0
  * `impact` = `null`
  * Use it when you need a default “no-fire” or “no-path” result.

***

## Static Methods

> **Note for designers**: Call `BallisticPath.Get(...)` from your C# scripts or via a debug gizmo to compute a full, sampled flight path before you actually fire the projectile.

```csharp
csharpCopyEditpublic static BallisticPath Get(
    Vector3 start,
    Collider startCollider,
    Vector3 velocity,
    float radius,
    float resolution,
    float maxLength,
    LayerMask collisionLayers,
    QueryTriggerInteraction queryTriggerInteraction = QueryTriggerInteraction.UseGlobal
)
```

1. **Purpose**\
   Perform a “spherecast‐based” ballistic simulation, stepping the projectile from `start` with initial `velocity` and under Unity’s built-in `Physics.gravity`. At each increment (defined by `resolution`), it checks for collisions against `collisionLayers`.
   * If a collision is detected, the returned path ends at that impact point and records the `RaycastHit`.
   * Otherwise, it traces forward up to `maxLength` and returns the full sampled path (possibly with `impact = null`).
2. **Parameters**
   * **`start`** (`Vector3`): World‐space origin of the projectile.
   * **`startCollider`** (`Collider`): The collider at launch (so that the algorithm can ignore immediate self-hits).
   * **`velocity`** (`Vector3`): Initial world‐space velocity vector (including direction and speed).
   * **`radius`** (`float`): Radius of the projectile’s “sphere” when sphere-casting. Use this if you want to approximate a projectile with a finite size.
   * **`resolution`** (`float`): Distance step between samples. Smaller values yield more granular sampling but cost more CPU. For example, `0.5f` means “step in 0.5-unit increments along the trajectory.”
   * **`maxLength`** (`float`): Maximum ray-distance to trace before giving up (e.g., 100 m).
   * **`collisionLayers`** (`LayerMask`): Layers to test for collision.
   * **`queryTriggerInteraction`** (`QueryTriggerInteraction`, optional): Whether to include trigger colliders in detection (default: `UseGlobal`).
3. **Returns**\
   A `BallisticPath` instance whose fields are:
   * `steps[]`: Every sampled `(position, velocity, time)` the simulator recorded until impact or until it ran out of `maxLength`.
   * `flightDistance`: Total path length along those samples.
   * `flightTime`: Time at the final sample (i.e., steps\[^1].time).
   * `impact`: If a collision happened, the `RaycastHit`; otherwise `null`.
4.  **Typical Usage**

    ```csharp
    csharpCopyEdit// Example: Previewing trajectory in OnDrawGizmos (or for aiming UI)
    void OnDrawGizmos()
    {
        if (Application.isPlaying)
        {
            Vector3 startPos = muzzleTransform.position;
            Vector3 launchVel = muzzleTransform.forward * muzzleSpeed;
            float radius = 0.1f;
            float resolution = 0.2f;
            float maxLen = 50f;
            LayerMask mask = LayerMask.GetMask("Default", "Environment");

            BallisticPath path = BallisticPath.Get(
                startPos,
                GetComponent<Collider>(),
                launchVel,
                radius,
                resolution,
                maxLen,
                mask
            );

            // Draw each sampled point in green, and mark impact point in red
            for (int i = 0; i < path.steps.Length; i++)
            {
                Gizmos.color = Color.green;
                Gizmos.DrawSphere(path.steps[i].position, radius * 0.5f);
            }

            if (path.impact.HasValue)
            {
                Gizmos.color = Color.red;
                Gizmos.DrawSphere(path.impact.Value.point, radius);
            }
        }
    }
    ```

***

## Instance Methods

* **`(Vector3 position, Vector3 velocity, float time) Lerp(float time)`**\
  Linearly interpolates between the two nearest sampled steps to return an approximate `(position, velocity, time)` at the requested `time` (seconds since launch).
  1. **Purpose**\
     Designers use `Lerp(..)` when they want to know exactly where (and how fast) the projectile is at an arbitrary moment along its flight—without having to manually find and blend two samples.
     * For example, you might spawn a trail effect or leave a decal at a specific elapsed time.
  2. **Parameter**
     * **`time`** (`float`): The desired elapsed‐time point in seconds.
       * If `time ≤ 0f`, returns the very first sample (`steps[0]`).
       * If `time ≥ flightTime`, returns the final sample (`steps[^1]`).
       * Otherwise, it finds the two adjacent samples whose `.time` bracket the requested `time`, then returns a blended tuple.
  3. **Returns**\
     A tuple `(position, velocity, time)`:
     * **`position`** – The interpolated world‐space position at the requested `time`.
     * **`velocity`** – The interpolated world‐space velocity at the requested `time`.
     * **`time`** – The same input `time` (clamped between 0 and `flightTime`).
  4.  **Typical Usage**

      ```csharp
      csharpCopyEdit// Suppose you want to know where the projectile will be exactly 0.75 seconds into the flight:
      BallisticPath path = /* obtain path via Get(...) */;
      float queryTime = 0.75f;
      var sample = path.Lerp(queryTime);
      Vector3 posAt075 = sample.position;
      Vector3 velAt075 = sample.velocity;
      // You can now position a debug marker, play an effect, etc.
      ```

***

## Designer Tips

* **Sampling Granularity (`resolution`)**
  * Lower `resolution` values (e.g., `0.1f`) yield more accurate arcs but more array entries (more memory/CPU).
  * Higher values (e.g., `0.5f` or `1.0f`) produce fewer samples but can miss fast, short collisions.
* **Collider Assignment (`startCollider`)**\
  Be sure to pass the same collider that your projectile will use at launch. That avoids immediately hitting yourself when the spherecast begins.
* **Visual Debugging**\
  Since `steps[]` is just a list of `(position, velocity, time)`, you can iterate it in `OnDrawGizmos` or in a custom Editor script to render lines, spheres, or arrows showing the entire flight arc before firing.
* **Checking for Hits**
  * If `impact` is non‐null, you know exactly which point/normal the projectile will hit and which `Collider` it intersects.
  * If it remains `null` and `flightDistance ≥ maxLength`, the projectile simply continued beyond your specified length without impact.
*   **Empty Path**\
    Use `BallisticPath.Empty` to initialize variables safely or to indicate “no trajectory yet.” For example:

    ```csharp
    csharpCopyEditprivate BallisticPath currentPath = BallisticPath.Empty;
    ```

    Then, after you fire or update, you assign it via `Get(...)`.

***

By using `BallisticPath.Get(...)` and `Lerp(...)`, designers can quickly compute, preview, and query full projectile trajectories—including sampling, collision detection, and interpolation—without writing manual raycasts or physics loops. This makes it easy to create aiming reticles, trajectory gizmos, and HUD indicators that respond accurately to gravity, speed, and scene geometry.
