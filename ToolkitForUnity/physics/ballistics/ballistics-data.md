# Ballistics Data

This is a helper struct used in many of our tools and has a 2D variant: `BallisticsData` encapsulates the core parameters needed to define and manipulate a projectile’s ballistic behavior. It holds the initial velocity vector and collision radius, and provides helper properties and methods for aiming (low‐ or high‐arc) and predicting full flight paths (used by `BallisticPath`).

***

## Public Fields

### Velocity

* **`public Vector3 velocity`**\
  The projectile’s current world‐space velocity vector (direction & magnitude).
  * Initially set this to something like `transform.forward * muzzleSpeed`.

### Radius

* **`public float radius`**\
  Radius (in world units) of the projectile—used for sphere‐casting when predicting collisions or following a path.
  * For a small bullet you might use `0.05f`; for a grenade, `0.2f`, etc.

***

## Public Properties

### Speed

* **`public float Speed { get; set; }`**
  * **Getter**: Returns `velocity.magnitude` (the current speed).
  * **Setter**: Normalizes `velocity` and multiplies by the assigned speed.
  *   **Designer Usage**:

      ```csharp
      csharpCopyEditBallisticsData data = new BallisticsData();
      data.Speed = 50f;                // Sets velocity to (same direction) * 50
      float currentSpeed = data.Speed; // Reads magnitude
      ```



### Direction

* **`public Vector3 Direction { get; set; }`**
  * **Getter**: Returns `velocity.normalized` (unit direction).
  * **Setter**: Keeps the current speed magnitude and replaces direction with the assigned vector.
  *   **Designer Usage**:

      ```csharp
      csharpCopyEditdata.Direction = Vector3.up; // Retains Speed, now pointing straight up
      ```



### Rotation

* **`public Quaternion Rotation { get; set; }`**
  * **Getter**: Returns a `Quaternion` that looks along `Direction` (i.e., `Quaternion.LookRotation(Direction)`).
  * **Setter**: Applies the assigned rotation’s forward vector (i.e., `rotation * Vector3.forward`) multiplied by the current `Speed`.
  *   **Designer Usage**:

      ```csharp
      csharpCopyEditdata.Rotation = Quaternion.Euler(0, 45, 0); 
      // Now velocity points at 45° yaw, with same magnitude as beforeublic Methods
      ```

***

## **Aiming Methods**

All `Aim` methods solve for a firing angle (using gravity or a constant acceleration) and immediately set `Rotation` so that `velocity` points along the chosen ballistic arc. They return `true` if a valid solution exists.

1.  **`public bool Aim(Vector3 from, Vector3 to)`**

    * **Description**: Computes a **low‐arc** firing solution from `from` (launch origin) to `to` (target position), under Unity’s default gravity (`Physics.gravity`).
    * **Success**: If there is at least one valid trajectory, it chooses the **lower‐angle** solution, sets `Rotation` accordingly (so that `velocity = forward * Speed` follows that arc), and returns `true`.
    * **Failure**: If no trajectory can hit the target (e.g., target out of range for the given `Speed`), returns `false` and leaves `Rotation` unchanged.

    ```csharp
    csharpCopyEdit// Example usage:
    BallisticsData data = new BallisticsData
    {
        Speed = 30f,
        radius = 0.1f
    };
    bool didAim = data.Aim(muzzlePosition, targetPosition);
    if (didAim)
    {
        // Now data.velocity is set to the correct low‐arc launch vector
        Instantiate(projectilePrefab, muzzlePosition, data.Rotation);
    }
    ```
2. **`public bool Aim(Vector3 from, Vector3 to, Vector3 constantAcceleration)`**
   * **Description**: Same as above, but uses `constantAcceleration` instead of `Physics.gravity`. Useful for custom gravity fields (e.g., 2D games, special zones).
   *   **Usage**:

       ```csharp
       csharpCopyEditVector3 fakeGravity = new Vector3(0, -5f, 0);
       bool aimed = data.Aim(playerPosition, enemyPosition, fakeGravity);
       ```
3. **`public bool AimHigh(Vector3 from, Vector3 to)`**
   * **Description**: Computes a **high‐arc** firing solution under default gravity. Uses the “high‐angle” solution (steeper angle).
   *   **Usage**:

       ```csharp
       csharpCopyEditif (data.AimHigh(cannonMuzzle, targetPoint))
       {
           // data.velocity now points along the high arc
       }
       ```
4. **`public bool AimHigh(Vector3 from, Vector3 to, Vector3 constantAcceleration)`**
   * **Description**: High‐arc solve under a custom acceleration vector.
   *   **Usage**:

       ```csharp
       csharpCopyEditVector3 customGravity = new Vector3(0, -20f, 0);
       bool canFireHigh = data.AimHigh(grenadeLauncherPos, enemyPos, customGravity);
       ```

***

## **Flight Prediction**

* **`public BallisticPath Predict(Vector3 from, Collider fromCollider, float resolution, float distanceLimit, LayerMask collisionLayers, QueryTriggerInteraction queryTriggerInteraction = QueryTriggerInteraction.UseGlobal, Vector3? constantAcceleration = null)`**
  1. **Purpose**\
     Simulate the projectile’s flight—sampling its position, velocity, and elapsed time at regular intervals—while also sphere‐casting to detect collisions (bounces or stops). Returns a `BallisticPath` struct containing all sampled steps, total distance, total time, and the first collision (if any).
  2. **Parameters**
     * **`Vector3 from`**: World‐space launch position.
     * **`Collider fromCollider`**: Collider to ignore on the first cast (typically the shooter’s collider).
     * **`float resolution`**: Sample spacing (in world units). Smaller → more samples, higher fidelity, more CPU.
     * **`float distanceLimit`**: Max path length before giving up (e.g., 50m).
     * **`LayerMask collisionLayers`**: Layers to test for collisions.
     * **`QueryTriggerInteraction queryTriggerInteraction`** (optional): Whether to include triggers.
     * **`Vector3? constantAcceleration`** (optional): Overrides Unity’s gravity. If `null`, uses `Physics.gravity`.
  3. **Behavior**
     * If `velocity == Vector3.zero`, returns `BallisticPath.Empty` (no path).
     * Otherwise, calls the internal `API.Ballistics.SphereCast(...)` routine under the hood (using `velocity`, `acceleration`, `radius`) to build a sampled path:
       * **`steps[]`**: Each entry is `(position, velocity, time)` at that sample.
       * **`flightDistance`**: Total distance traveled to the last sample.
       * **`flightTime`**: Time of the last sample (taken from `steps[^1].time`).
       * **`impact`**: If the sphere‐cast detected a hit, this is the `RaycastHit`; otherwise `null`.
  4.  **Returns**\
      A fully constructed `BallisticPath`, which you can then pass to `BallisticPathFollow` or use for drawing/editing:

      ```csharp
      csharpCopyEditBallisticPath result = data.Predict(
          launchPos,
          shooterCollider,
          0.1f,             // resolution
          50f,              // distance limit
          LayerMask.GetMask("Environment"),
          QueryTriggerInteraction.Ignore,
          Physics.gravity   // or a custom gravity vector
      );
      // Now result.steps is an array of sampled points, velocities, and times.
      ```

***

## Designer & Programmer Tips

*   **Initialize `velocity` Directly**\
    You can bypass `Speed`/`Direction` and set `velocity` directly if you already know the full vector. Example:

    ```csharp
    csharpCopyEditdata.velocity = new Vector3(10f, 15f, 0f); // X=10, Y=15, Z=0
    data.radius = 0.2f;
    ```
* **Using `Speed`, `Direction`, and `Rotation`**
  * **`data.Speed = 20f;`** → Maintains current direction but changes speed to 20.
  * **`data.Direction = Vector3.up;`** → Keeps the same speed, now pointing straight up.
  * **`data.Rotation = Quaternion.Euler(0, 30, 0);`** → Sets `velocity` to `(forward-of-30°) * existing Speed`.
* **Choosing Low vs. High Arc**
  * **Low Arc (`Aim`)** → Flatter trajectory, faster time of flight, less drop—ideal for direct shots.
  * **High Arc (`AimHigh`)** → Steeper trajectory, longer airtime—useful for clearing obstacles or firing over hills.
* **Custom Gravity**
  * If you’re working in a space environment or simulating different gravitational pull, call the overload with `constantAcceleration`.
  *   E.g., for a moon‐like environment with weaker gravity:

      ```csharp
      csharpCopyEditVector3 moonGravity = new Vector3(0, -1.62f, 0);
      data.Aim(launcherPos, targetPos, moonGravity);
      ```
* **Predicting Before Instantiation**
  * Run `Predict(...)` in an `OnDrawGizmos` or preview mode to display the full arc before actually spawning a physical projectile.
  * Use the returned `BallisticPath` to draw lines, place UI markers, or schedule sounds/effects at predicted collision points.
* **Collision Radius**
  * If your projectile is essentially a ray (e.g., bullet), set `radius = 0f`.
  * For objects like grenades or balls, choose a radius matching the model’s approximate size (e.g., `0.25f`).
* **Handling Zero‐Velocity**
  * If you forget to set `Speed` (leaving `velocity == Vector3.zero`), `Predict(...)` immediately returns an empty path—no crash, but nothing happens. Keep an eye on runtime logs or guard before calling.
