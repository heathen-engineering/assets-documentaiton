# API.Ballistics

The `Ballistics` class (namespace `Heathen.UnityPhysics.API`) offers a comprehensive set of static methods for solving projectile‐motion problems in both 3D and 2D contexts. Designers and programmers can use these utilities to:

* Estimate maximum range or required speed/angle.
* Compute flight time or final velocity for a given trajectory.
* Solve for launch rotations (low/high arc) toward stationary or moving targets.
* Generate full, sampled trajectories via raycasts or spherecasts that account for gravity or other constant accelerations.

Below is a grouped reference of all public methods, with usage notes, parameter descriptions, and practical tips.

***

## 1. Maximum Range & Flight Time

### 1.1 MaxRange (3D)

```csharp
public static float MaxRange(float speed, float gravity, float height)
```

* **Purpose**: Returns the maximum horizontal distance (range) reachable when launching at 45° from a given height, ignoring air resistance.
* **Parameters**:
  * `speed` (float): Initial launch speed (> 0).
  * `gravity` (float): Gravity magnitude (> 0).
  * `height` (float): Launch‐point height above the landing plane (≥ 0).
* **Returns**:
  * Maximum range (units), or 0 if invalid inputs (`speed ≤ 0`, `gravity ≤ 0`, or `height < 0`).
* **Usage**:
  * Quickly gauge how far a cannonball or grenade would travel when fired at 45°.
  * Clamp AI or camera aiming—e.g., if `targetDistance > MaxRange(speed, 9.81f, muzzleHeight)`, skip the shot.

***

```csharp
public static float FlightTime(
    Vector3 start,
    Vector3 end,
    Vector3 velocity,
    Vector3 constantAcceleration,
    float tolerance = 0.01f
)
```

* **Purpose**: Finds a positive flight time `t` such that the projectile, launched from `start` with initial `velocity` and subjected to `constantAcceleration`, arrives at `end`.
* **Parameters**:
  * `start`, `end` (Vector3): World‐space start and end positions.
  * `velocity` (Vector3): Initial velocity vector.
  * `constantAcceleration` (Vector3): Constant acceleration (e.g., `(0, –9.81f, 0)`).
  * `tolerance` (float): Maximum allowed error when comparing solutions on each axis (default `0.01`).
* **Returns**:
  * A positive flight time (seconds) if a consistent solution across X/Y/Z axes is found; otherwise `float.NaN`.
* **Usage**:
  * Determine “time to impact” given a known launch vector—useful for synchronizing timed effects.
  * Validate a precomputed trajectory—if `FlightTime(...)` returns `NaN`, there is no way to reach `end` with the given inputs.

***

### 1.3 FlightTime2D (2D)

```csharp
public static float FlightTime2D(
    Vector2 start,
    Vector2 end,
    Vector2 velocity,
    Vector2 constantAcceleration,
    float tolerance = 0.01f
)
```

* **Purpose**: Same as `FlightTime` but in the X/Y plane (2D).
* **Parameters**:
  * `start`, `end` (Vector2): 2D start and end positions.
  * `velocity` (Vector2): Initial 2D velocity.
  * `constantAcceleration` (Vector2): 2D acceleration.
  * `tolerance` (float): Allowed difference between X and Y solutions (default `0.01`).
* **Returns**:
  * Positive flight time if a consistent solution exists; otherwise `NaN`.
* **Usage**:
  * Pinpoint when a 2D projectile reaches a specific point (e.g., for triggering splash effects).

***

### 1.4 FinalVelocity (3D)

```csharp
public static Vector3 FinalVelocity(
    Vector3 initialVelocity,
    Vector3 constantAcceleration,
    float flightTime
)
```

* **Purpose**: Computes the final velocity after time `flightTime` under constant acceleration.
* **Returns**: `initialVelocity + constantAcceleration * flightTime`.
* **Usage**:
  * After computing flight time via `FlightTime`, call this to know the speed/direction at impact.

***

### 1.5 FinalVelocity2D (2D)

```csharp
public static Vector2 FinalVelocity2D(
    Vector2 initialVelocity,
    Vector2 constantAcceleration,
    float flightTime
)
```

* **Purpose**: 2D analog of `FinalVelocity`.
* **Returns**: `initialVelocity + constantAcceleration * flightTime`.

***

## 2. Launch‐Angle Solutions (Stationary Targets)

These methods solve for one or two possible launch rotations (quaternions) that send a projectile from `projectile` to `target`, given speed or gravity. They return the number of valid solutions (0, 1, or 2), and output `lowAngle` (flatter trajectory) and `highAngle` (steeper trajectory). In 3D, you can supply a full acceleration vector; in 2D, analogous methods operate on Vector2.

***

### 2.1 Solution (3D with Constant Acceleration)

```csharp
public static int Solution(
    Vector3 projectile,
    float speed,
    Vector3 target,
    Vector3 constantAcceleration,
    out Quaternion lowAngle,
    out Quaternion highAngle
)
```

* **Purpose**: Solves for low‐ and high‐arc launch rotations when acceleration may not be purely vertical (e.g., gravity + wind).
* **Algorithm**:
  1. Rotate world so `constantAcceleration` aligns with `(0, –1, 0)`.
  2. Solve 2D problem in that space with scalar gravity = ‖`constantAcceleration`‖.
  3. Rotate solutions back to original space.
* **Parameters**:
  * `projectile`, `target`: World‐space positions.
  * `speed`: Scalar launch speed (> 0).
  * `constantAcceleration`: Any nonzero acceleration vector.
* **Returns**:
  * `0` if no solutions (e.g., out of range or zero acceleration), `1` if a single tangent, or `2` if two distinct arcs exist.
  * `lowAngle`/`highAngle` are set to identity if no solutions; otherwise, the corresponding quaternions.
*   **Usage**:

    ```csharp
    if (Ballistics.Solution(muzzlePos, muzzleSpeed, enemyPos, Physics.gravity, out Quaternion low, out Quaternion high) > 0)
    {
        // Use low or high: e.g., turret.rotation = low;
    }
    ```
* **Designer Tips**:
  * Use low‐arc (`lowAngle`) for faster, direct shots.
  * Use high‐arc (`highAngle`) for lobbed trajectories (e.g., launching over obstacles).

***

### 2.2 Solution2D (2D with Constant Acceleration)

```csharp
public static int Solution2D(
    Vector2 projectile,
    float speed,
    Vector2 target,
    Vector2 constantAcceleration,
    out Quaternion lowAngle,
    out Quaternion highAngle
)
```

* **Purpose**: 2D equivalent of the above, returning quaternions whose forward vector lies in the XY‐plane.
* **Parameters**:
  * `projectile`, `target` (Vector2): 2D start and end.
  * `constantAcceleration`: Typically `(0, –gravity)`.
* **Returns**:
  * Number of solutions (0, 1, or 2).
  * `lowAngle`, `highAngle` quaternions (their “forward” points in the 2D direction of launch).
*   **Usage**:

    ```csharp
    if (Ballistics.Solution2D(
            new Vector2(barrelX, barrelY),
            launchSpeed,
            new Vector2(enemyX, enemyY),
            new Vector2(0, -9.81f),
            out Quaternion lowQ,
            out Quaternion highQ))
    {
        // Apply lowQ to a 2D sprite’s rotation (using Quaternion.LookRotation)
    }
    ```

***

### 2.3 Solution (3D with Gravity Scalar)

```csharp
public static int Solution(
    Vector3 projectile,
    float speed,
    Vector3 target,
    float gravity,
    out Quaternion lowAngle,
    out Quaternion highAngle
)
```

* **Purpose**: Classic 3D ballistic‐trajectory solver assuming vertical gravity of magnitude `gravity`. Returns quaternions for low/high launch angles.
* **Parameters**:
  * `projectile`, `target`: World‐space positions.
  * `speed`: Initial speed (> 0).
  * `gravity`: Gravity magnitude (> 0).
* **Returns**:
  * `0` if no real solutions (target out of range), `1` if tangent, or `2` if two distinct arcs.
  * `lowAngle` = flatter arc; `highAngle` = steeper arc.
*   **Usage**:

    ```csharp
    int solutions = Ballistics.Solution(
        muzzlePos, muzzleSpeed, enemyPos,
        Physics.gravity.y * -1f,  // Provide positive gravity scalar
        out Quaternion low, out Quaternion high
    );
    if (solutions > 0) turret.rotation = low;
    ```

***

### 2.4 Solution2D (2D with Gravity Scalar)

```csharp
public static int Solution2D(
    Vector2 projectile,
    float speed,
    Vector2 target,
    float gravity,
    out Quaternion lowAngle,
    out Quaternion highAngle
)
```

* **Purpose**: 2D analog of the 3D‐gravity solver.
* **Returns**: Low/high quaternions whose forward axis is `(0,0,1)` and “up” is the 2D launch vector in XY.
*   **Usage**:

    ```csharp
    int sols = Ballistics.Solution2D(
        new Vector2(barrelX, barrelY),
        launchSpeed,
        new Vector2(enemyX, enemyY),
        9.81f,
        out Quaternion lowQ,
        out Quaternion highQ
    );
    if (sols > 0) sprite.transform.rotation = lowQ;
    ```

***

## 3. Aiming Solutions (Moving Targets)

When the target moves with a constant velocity, these methods solve a quartic equation for time of intercept and compute the corresponding launch directions. They support both 3D and 2D.

***

### 3.1 Solution (3D, Moving Target)

```csharp
public static int Solution(
    Vector3 projectile,
    float speed,
    Vector3 target,
    Vector3 targetVelocity,
    float gravity,
    out Quaternion lowAngle,
    out Quaternion highAngle
)
```

* **Purpose**: Finds up to two valid launch rotations that intercept a target moving at `targetVelocity` under scalar vertical gravity.
* **Algorithm**:
  1. Build quartic coefficients for intercept time `t` based on relative positions and velocities (derived from “lib\_fts” formulas).
  2. Solve quartet for positive roots.
  3. For each positive root `t`, compute required launch velocity vector.
  4. Convert those direction vectors into quaternions (`Quaternion.LookRotation(...)`).
* **Parameters**:
  * `projectile`, `target`: Initial positions.
  * `speed`: Launch speed.
  * `targetVelocity`: Constant world‐space velocity of the target.
  * `gravity`: Gravity magnitude (> 0).
* **Returns**:
  * Count `count` of valid launch‐vectors (0, 1, or 2).
  * `lowAngle` = first solution; `highAngle` = second solution if present, otherwise same as `lowAngle`.
*   **Usage**:

    ```csharp
    int n = Ballistics.Solution(
        muzzlePos, launchSpeed, enemyPos, enemyVel,
        9.81f, out Quaternion aimLow, out Quaternion aimHigh
    );
    if (n > 0) turret.rotation = aimLow;
    ```

***

### 3.2 Solution2D (2D, Moving Target)

```csharp
public static int Solution2D(
    Vector2 projectile,
    float speed,
    Vector2 target,
    Vector2 targetVelocity,
    float gravity,
    out Quaternion lowAngle,
    out Quaternion highAngle
)
```

* **Purpose**: 2D counterpart for a moving target on the X/Y plane under vertical gravity.
* **Returns**:
  * Number of valid solutions (0, 1, 2).
  * Quaternions whose forward is `(0,0,1)` and up‐vector corresponds to the required 2D launch vector.
*   **Usage**:

    ```csharp
    int solutions = Ballistics.Solution2D(
        new Vector2(barrelX, barrelY),
        launchSpeed,
        new Vector2(enemyX, enemyY),
        new Vector2(enemyVelX, enemyVelY),
        9.81f,
        out Quaternion lowQ,
        out Quaternion highQ
    );
    if (solutions > 0) my2DSprite.rotation = lowQ;
    ```

***

## 4. Arc‐Ceiling Solutions (Fixed and Moving Targets)

These methods compute the initial velocity vector and required gravity to satisfy a specified “maximum height” (arc ceiling) along the trajectory, solving a system of equations that force the apex of the parabola to reach `arcCeiling`. Both 3D and 2D variants exist, for stationary and moving targets.

***

### 4.1 Solution (3D, Prescribed Arc Ceiling, Stationary Target)

```csharp
public static bool Solution(
    Vector3 projectile,
    float linearSpeed,
    Vector3 target,
    float arcCeiling,
    out Vector3 firingVelocity,
    out float gravity
)
```

* **Purpose**: Given a desired apex height (`arcCeiling`) and constant horizontal speed (`linearSpeed`), finds the vertical component of the initial velocity and gravity value needed to pass through that apex and land at `target`.
* **Parameters**:
  * `projectile`, `target`: World‐space start and end.
  * `linearSpeed`: Speed along the horizontal plane (XZ).
  * `arcCeiling`: Desired maximum height (absolute Y value) of the trajectory, must be > `projectile.y`.
* **Outputs**:
  * `firingVelocity`: Vector3 launch velocity (combining horizontal direction and vertical component).
  * `gravity`: Negative gravity scalar required to achieve that apex.
* **Returns**: `true` if a valid solution exists; `false` otherwise (e.g., `projectile == target`, `arcCeiling ≤ projectile.y`, or zero horizontal distance).
*   **Usage**:

    ```csharp
    if (Ballistics.Solution(
            muzzlePos, 10f, targetPos,
            15f,         // apex at Y = 15
            out Vector3 launchVel,
            out float neededGravity))
    {
        // Use launchVel as initial velocity; apply gravity = neededGravity downward
    }
    ```

***

### 4.2 Solution2D (2D, Prescribed Arc Ceiling, Stationary Target)

```csharp
public static bool Solution2D(
    Vector2 projectile,
    float linearSpeed,
    Vector2 target,
    float arcCeiling,
    out Vector2 firingVelocity,
    out float gravity
)
```

* **Purpose**: Same as above, but in 2D (X/Y).
*   **Usage**:

    ```csharp
    if (Ballistics.Solution2D(
            new Vector2(barrelX, barrelY),
            8f,                                      // horizontal speed
            new Vector2(enemyX, enemyY),
            barrelY + 5f,                            // apex 5 units above barrel
            out Vector2 launchVel2D,
            out float neededG2D))
    {
        // Use launchVel2D.y and apply gravity = neededG2D
    }
    ```

***

### 4.3 Solution (3D, Prescribed Arc Ceiling, Moving Target)

```csharp
public static bool Solution(
    Vector3 projectile,
    float linearSpeed,
    Vector3 target,
    Vector3 targetVelocity,
    float arcCeiling,
    out Vector3 firingVelocity,
    out float gravity,
    out Vector3 impactPoint
)
```

* **Purpose**: Computes initial `firingVelocity` and `gravity` so the projectile intercepts a moving target at a trajectory whose apex is `arcCeiling` above max(startY, targetY). Also returns the computed `impactPoint` accounting for movement.
* **Parameters**:
  * `projectile`: Launch position.
  * `linearSpeed`: Horizontal speed on the XZ plane (no vertical component).
  * `target`, `targetVelocity`: Initial position and velocity of the moving target.
  * `arcCeiling`: Desired apex height above “ground”—calculated as `max(projectile.y, impactPoint.y) + arcCeiling`.
* **Outputs**:
  * `firingVelocity` (Vector3): Initial velocity (both horizontal and vertical components).
  * `gravity` (float): Negative gravity scalar needed.
  * `impactPoint` (Vector3): World‐space point where the projectile collides, given the target’s motion.
* **Returns**: `true` if a valid intercept solution exists; `false` otherwise.
*   **Usage**:

    ```csharp
    if (Ballistics.Solution(
            muzzlePos, 12f,
            enemyPos, enemyVel,
            10f,                    // apex 10 units above
            out Vector3 launchVel3D,
            out float neededG3D,
            out Vector3 intercept))
    {
        // Apply launchVel3D and set gravity = neededG3D
        // You can also visualize intercept
    }
    ```

***

### 4.4 Solution2D (2D, Prescribed Arc Ceiling, Moving Target)

```csharp
public static bool Solution2D(
    Vector2 projectile,
    float linearSpeed,
    Vector2 target,
    Vector2 targetVelocity,
    float arcCeiling,
    out Vector2 firingVelocity,
    out float gravity,
    out Vector2 impactPoint
)
```

* **Purpose**: 2D version of the moving‐target, prescribed apex solver.
*   **Usage**:

    ```csharp
    if (Ballistics.Solution2D(
            new Vector2(barrelX, barrelY),
            7f,
            new Vector2(enemyX, enemyY),
            new Vector2(enemyVelX, 0),  // only horizontal velocity matters
            5f,
            out Vector2 launchVel2D,
            out float g2D,
            out Vector2 intercept2D))
    {
        // Fire with launchVel2D and apply gravity = g2D
    }
    ```

***

## 5. Flight‐Time Specified Solutions

When you know exactly how long you want the projectile to be in flight (e.g., for timing or syncing purposes), these methods compute the required initial velocity to land at `target` after a fixed `flightTime` under a constant gravity.

***

### 5.1 Solution (3D, Flight Time Specified)

```csharp
public static Vector3 Solution(
    Vector3 projectile,
    Vector3 target,
    float gravity,
    float flightTime
)
```

* **Purpose**: Returns the initial velocity vector that sends a projectile from `projectile` to `target` in exactly `flightTime`, under vertical gravity of magnitude `gravity`.
* **Parameters**:
  * `projectile`, `target`: World positions.
  * `gravity`: Gravity scalar (negative or positive? It uses `gravity` as is, so typically pass a negative value, e.g., `-9.81f`).
  * `flightTime`: Desired time to impact (> 0).
* **Returns**:
  * A `Vector3` whose horizontal components (`x,z`) equal `horizontalDistance / flightTime`, and whose vertical component solves `y0 + vy*t + 0.5*gravity*t^2 = y1`.
*   **Usage**:

    ```csharp
    Vector3 requiredVel = Ballistics.Solution(
        startPos, endPos,
        -9.81f,    // negative gravity
        2.5f       // hit target in 2.5 seconds
    );
    // Use requiredVel as the projectile’s initial velocity
    ```

***

### 5.2 Solution2D (2D, Flight Time Specified)

```csharp
public static Vector2 Solution2D(
    Vector2 projectile,
    Vector2 target,
    float gravity,
    float flightTime
)
```

* **Purpose**: 2D analog (X/Y) for fixed `flightTime`.
* **Returns**: `Vector2(horizontalVelocity, verticalVelocity)`.
*   **Usage**:

    ```csharp
    Vector2 launchVel2D = Ballistics.Solution2D(
        new Vector2(barrelX, barrelY),
        new Vector2(enemyX, enemyY),
        -9.81f,
        1.8f    // seconds
    );
    ```

***

## 6. Speed‐Given‐Angle Solutions

These methods compute the necessary launch speed (magnitude) to hit a `target` from `projectile` when the launch direction is constrained to a fixed angle `angleDegrees` above the horizontal.

***

### 6.1 Solution (3D, Speed Given Angle)

```csharp
public static bool Solution(
    Vector3 projectile,
    Vector3 target,
    float angleDegrees,
    float gravity,
    out float speed
)
```

* **Purpose**: With a fixed elevation `angleDegrees` (above the horizontal plane), computes the required scalar `speed` so the projectile reaches `target` under vertical gravity of magnitude `gravity`.
* **Parameters**:
  * `projectile`, `target`: Start and end positions.
  * `angleDegrees`: Launch angle from horizontal (0–90).
  * `gravity`: Gravity magnitude (> 0).
* **Outputs**:
  * `speed`: Required launch speed.
* **Returns**: `true` if a valid (real) solution exists; `false` otherwise (e.g., denominator ≥ 0 or range = 0).
*   **Usage**:

    ```csharp
    if (Ballistics.Solution(
            turretPos, enemyPos,
            30f,      // 30° elevation
            9.81f, 
            out float neededSpeed))
    {
        // Fire with muzzle velocity = neededSpeed, pointing at angleDegrees above the horizontal
    }
    ```

***

### 6.2 Solution2D (2D, Speed Given Angle)

```csharp
public static bool Solution2D(
    Vector2 projectile,
    Vector2 target,
    float angleDegrees,
    float gravity,
    out float speed
)
```

* **Purpose**: 2D version for a fixed launch angle in X/Y.
* **Returns**:
  * Required speed magnitude, combining horizontal component `z` and vertical component `y`.
*   **Usage**:

    ```csharp
    if (Ballistics.Solution2D(
            new Vector2(barrelX, barrelY),
            new Vector2(enemyX, enemyY),
            45f,
            9.81f,
            out float speed2D))
    {
        // Fire from barrel with speed2D at 45° up
    }
    ```

***

## 7. Trajectory Marching (Raycast & SphereCast)

These methods allow you to “march” a projectile along its path—applying constant acceleration at each step—and perform either raycasts or spherecasts to detect collisions. They return both the impact (if any) and a sampled path of `(position, velocity, time)` tuples.

***

### 7.1 Raycast (3D)

```csharp
public static bool Raycast(
    Vector3 start,
    Vector3 velocity,
    Vector3 constantAcceleration,
    float resolution,
    float maxLength,
    LayerMask collisionLayers,
    out RaycastHit hit,
    out List<(Vector3 position, Vector3 velocity, float time)> path,
    out float distance
)
```

* **Purpose**: Step through a parabolic path, using a symmetric ray at each segment of length `resolution`, to detect the first collision.
* **Parameters**:
  * `start`: Starting position (Vector3).
  * `velocity`: Initial launch vector.
  * `constantAcceleration`: Gravity or other acceleration.
  * `resolution`: Step length between raycasts (e.g., `0.1f`).
  * `maxLength`: Maximum total arc‐length to march.
  * `collisionLayers`: LayerMask for collision detection.
* **Outputs**:
  * `hit`: The `RaycastHit` if collision occurred (otherwise `hit.transform == null`).
  * `path`: A `List` of tuples `(position, velocity, time)`, starting with `(start, velocity, 0f)`, then each sampled point until impact or until exceeding `maxLength`.
  * `distance`: Total distance traveled along the curve before impact (or `maxLength` if no hit).
* **Returns**: `true` if a collision was detected; `false` otherwise.
*   **Usage**:

    ```csharp
    if (Ballistics.Raycast(
            muzzlePos,
            launchVel,
            Physics.gravity,
            0.2f,                  // resolution
            50f,                   // maxLength
            LayerMask.GetMask("Walls"),
            out RaycastHit info3D,
            out var sampledPath3D,
            out float traveledDist
    ))
    {
        // sampledPath3D contains the positions & velocities at each step,
        // info3D.point is the impact point, and traveledDist is the arc length.
    }
    ```
* **Designer Tips**:
  * Use for custom trajectory visualizers or to spawn effects at predicted impact.
  * Remember that smaller `resolution` values yield smoother curves and more accurate collision detection at higher CPU cost.

***

### 7.2 SphereCast (3D)

```csharp
public static bool SphereCast(
    Vector3 start,
    Collider startCollider,
    Vector3 velocity,
    Vector3 constantAcceleration,
    float radius,
    float resolution,
    float maxLength,
    LayerMask collisionLayers,
    QueryTriggerInteraction queryTriggerInteraction,
    out RaycastHit hit,
    out List<(Vector3 position, Vector3 velocity, float time)> path,
    out float distance
)
```

* **Purpose**: Similar to `Raycast(...)`, but uses a sphere of radius `radius` to detect collisions, checking against `collisionLayers` with optional trigger inclusion. Temporarily disables `startCollider` at the very beginning to avoid self‐hits.
* **Parameters**:
  * `startCollider`: The `Collider` to disable at launch until the projectile moves beyond its radius, preventing immediate self‐collision. May be `null`.
  * All others match `Raycast(...)` with the addition of `radius` and `queryTriggerInteraction`.
*   **Usage**:

    ```csharp
    if (Ballistics.SphereCast(
            muzzlePos,
            muzzleCollider,
            launchVel,
            Physics.gravity,
            0.1f,                  // sphere radius
            0.2f,                  // resolution
            50f,
            LayerMask.GetMask("Obstacles"),
            QueryTriggerInteraction.Ignore,
            out RaycastHit sphereHit,
            out var spherePath,
            out float sphereDist
    ))
    {
        // path includes the hit point; sphereHit provides normal, collider, etc.
    }
    ```

***

### 7.3 Raycast2D (2D)

```csharp
public static bool Raycast2D(
    Vector2 start,
    Vector2 velocity,
    Vector2 constantAcceleration,
    float resolution,
    float maxLength,
    LayerMask collisionLayers,
    out RaycastHit2D hit,
    out List<(Vector2 position, Vector2 velocity, float time)> path,
    out float distance
)
```

* **Purpose**: Marches a 2D projectile along its XY path via `Physics2D.Raycast` at each step of length `resolution`, accumulating `(position, velocity, time)` samples until impact or until the traveled distance ≥ `maxLength`.
*   **Usage**:

    ```csharp
    if (Ballistics.Raycast2D(
            new Vector2(barrelX, barrelY),
            launchVel2D,
            new Vector2(0, -9.81f),
            0.05f,                  // resolution
            30f,                    // maxLength
            LayerMask.GetMask("Platform"),
            out RaycastHit2D hit2D,
            out var path2D,
            out float dist2D
    ))
    {
        // path2D holds sampled points; hit2D has collision info.
    }
    ```

***

### 7.4 CircleCast (2D)

```csharp
public static bool CircleCast(
    Vector2 start,
    Collider2D startCollider,
    Vector2 velocity,
    Vector2 constantAcceleration,
    float radius,
    float resolution,
    float maxLength,
    LayerMask collisionLayers,
    out RaycastHit2D hit,
    out List<(Vector2 position, Vector2 velocity, float time)> path,
    out float distance
)
```

* **Purpose**: 2D analog of `SphereCast(...)`. At each incremental step of length `resolution`, performs `Physics2D.CircleCast` with radius `radius` (temporarily disabling `startCollider` to avoid self‐hit).
*   **Usage**:

    ```csharp
    if (Ballistics.CircleCast(
            new Vector2(barrelX, barrelY),
            barrelCollider2D,
            launchVel2D,
            new Vector2(0, -9.81f),
            0.2f,                   // radius
            0.05f,                  // resolution
            30f,
            LayerMask.GetMask("Enemy"),
            out RaycastHit2D circleHit,
            out var circlePath,
            out float circleDist
    ))
    {
        // circlePath contains the sampled trajectory, ending with the impact point.
    }
    ```

***

### 7.5 SphereCast (Simplified Overload, 3D)

```csharp
public static bool SphereCast(
    Vector3 start,
    Collider startCollider,
    Vector3 velocity,
    float radius,
    float resolution,
    float maxLength,
    LayerMask collisionLayers,
    QueryTriggerInteraction queryTriggerInteraction,
    out RaycastHit hit,
    out List<(Vector3 position, Vector3 velocity, float time)> path,
    out float distance
)
```

* **Purpose**: A single‐spherecast version that marches only in one long cast of length `maxLength` (rather than incremental steps). It still disables `startCollider` briefly to prevent self‐collision.
* **Behavior**:
  1. Disable `startCollider`.
  2. Perform a single `Physics.SphereCast(ray, radius, maxLength, collisionLayers, queryTriggerInteraction)`.
  3. If hit, compute `hitTime = (hitPoint – start).magnitude / velocity.magnitude`, add `(hitPoint, velocity, hitTime)` to `path`, set `distance = (hitPoint – start).magnitude`, and return `true`.
  4. If no hit, restore `startCollider`, set `distance = maxLength`, return `false`.
*   **Usage**:

    ```csharp
    if (Ballistics.SphereCast(
            startPos,
            myCollider,
            initVel,
            0.1f, 
            0.01f,
            20f,
            LayerMask.GetMask("Terrain"),
            QueryTriggerInteraction.Collide,
            out RaycastHit hitInfo,
            out var simplePath,
            out float simpleDist
    ))
    {
        // simplePath contains only two entries: start and impact point.
    }
    else
    {
        // No collision within maxLength.
    }
    ```

***

## Usage Scenarios & Tips

1. **Quick Range Checks**
   * Use `MaxRange(speed, gravity, height)` to decide if a target is out of theoretical range before attempting a more expensive solution.
2. **Single‐Frame Aim**
   *   For a turret that does not account for target motion:

       ```csharp
       if (Ballistics.Solution(
               turretPos, turretSpeed, targetPos,
               Physics.gravity.y * -1f, 
               out Quaternion low, out Quaternion high))
       {
           turret.rotation = low;
       }
       ```
3. **Moving Target Intercept**
   *   To lead a moving enemy, call the 3D “moving target” solver:

       ```csharp
       int n = Ballistics.Solution(
           turretPos, turretSpeed,
           enemyPos, enemyVelocity,
           9.81f,
           out Quaternion lowLead, out Quaternion highLead
       );
       if (n > 0) turret.rotation = lowLead;
       ```
4. **Trajectory Visualization**
   *   To draw a predictive line or spawn tracer particles along the path:

       ```csharp
       Ballistics.SphereCast(
           launchPos, shooterCollider, launchVel,
           gravityVector,
           sphereRadius,
           sampleResolution,
           maxArcLength,
           layerMask,
           QueryTriggerInteraction.Ignore,
           out RaycastHit collisionInfo,
           out var fullPath,
           out float arcDist
       );
       // fullPath is a List<(position, velocity, time)>—use position for gizmos.
       ```
5. **Planned Bounce Calculations**
   *   Combine `SphereCast(...)` with `Ballistics.Solution(...)` for successive bounces:

       ```csharp
       // 1. Initial arc (maybe no bounce):
       Ballistics.SphereCast(start, myCollider, vel, grav, radius, res, maxLen, layers,
           QueryTriggerInteraction.Ignore, out var hit0, out var path0, out var dist0);

       // 2. If hit0.transform != null:
       Vector3 reflectVel = Vector3.Reflect(path0[^1].velocity, hit0.normal) * 0.8f;
       Vector3 newStart = hit0.point;
       Ballistics.SphereCast(newStart, myCollider, reflectVel, grav, radius, res, maxLen2, layers,
           QueryTriggerInteraction.Ignore, out var hit1, out var path1, out var dist1);
       ```
   * Append `path1` to `path0` if you wish to visualize or feed into a “follow‐path” component.
6. **Custom Gravity or Other Constant Forces**
   * Any method that takes `constantAcceleration` (Vector3/Vector2) can simulate wind, buoyancy, or magnetic forces by changing `constantAcceleration` from `(0, –9.81f, 0)` to something else (e.g., `(2f, –5f, 0)`).
7. **Prescribed Apex Height**
   * When you want a projectile’s highest point to be at a specific Y, use the arc‐ceiling solvers. This is especially useful for:
     * Curved arrow shots over cover.
     * Jump arcs for AI characters (treat them as “projectiles”).
8. **Fixed Flight Time**
   * If you need the projectile to take exactly `t` seconds to reach the target (e.g., synchronized explosion), use `Solution(start, target, gravity, flightTime)`.
9. **Error Handling**
   * Always check return booleans or solution counts. If a solver returns `false` or `0`, either the target is out of range, the angle/speed combination is impossible, or parameters are invalid (e.g., zero speed or zero gravity).
