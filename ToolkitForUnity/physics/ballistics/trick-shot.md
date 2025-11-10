# Trick Shot

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

TrickShot and TrickShot2D have the same basic setup and functionality 1 for 3D space and 1 for 2D space: `TrickShot` lets designers compute and visualize a multi‐bounce ballistic trajectory at runtime (storing it in `prediction`) and then spawn a `BallisticPathFollow` prefab along that exact path via `Shoot()`. It’s ideal for “grenade launcher”–style weapons or any projectile that should follow a precomputed arc with optional bounces.

***

## Public Fields

### Speed

* **`float speed`**\
  Initial launch speed (units/sec). Combined with `transform.forward` to form the launch velocity.

### Constant Acceleration

* **`Vector3 constantAcceleration`**\
  Gravity or custom acceleration applied throughout flight. Defaults to `(0, –9.81f, 0)`.

### Radius

* **`float radius`**\
  Sphere‐cast radius used when predicting collisions. Set this to roughly match your projectile’s size.

### Template

* **`BallisticPathFollow template`**\
  A reference to a prefab (or scene object) that has `BallisticPathFollow` on it.
  * At `Shoot()`, this prefab is instantiated, and its `projectile` and `path` fields are filled using the computed `prediction`.

### Resolution

* **`float resolution`** (minimum `0.01`)\
  Sampling increment for each prediction segment. Smaller values → finer trajectory at higher CPU cost.

### Distance

* **`float distance`**\
  Maximum trace length per segment (or total, see `distanceIsTotalLength`).

### Collision Layers

* **`LayerMask collisionLayers`**\
  Layers used for collision detection when predicting. Only colliders on these layers will register impacts.

### Trigger Interaction

* **`QueryTriggerInteraction triggerInteraction`**\
  Whether to include triggers in collision checks (`UseGlobal`, `Ignore`, or `Collide`).

### Bounces

* **`int bounces`**\
  Number of allowed bounces after the first impact. Set to 0 for a single arc, >0 to simulate up to N bounces.

### Bounce Damping

* **`float bounceDamping`** (`[0, 1]`)\
  Fraction of velocity lost on each bounce. A value of 0.5 means the reflected velocity is halved after impact.

### Distance Is Total Length

* **`bool distanceIsTotalLength`**
  * **`false` (default)** – Each segment’s `Predict()` uses `distance` as its own distance limit.
  * **`true`** – After each bounce, subtract that segment’s `flightDistance` from `distance`, so `distance` becomes the maximum total arc length across all segments.

### Prediciton

* **`List<BallisticPath> prediction`**\
  The computed list of `BallisticPath` segments. After calling `Predict()`, this list holds one entry per segment (first arc plus each bounce arc). Designers can inspect or draw these paths before spawning.

***

## Public Methods

### Predict

**`void Predict()`**

Compute and store a full, multi‐bounce trajectory in `prediction`.

**Workflow**

1. Creates a local `BallisticsData` with:
   * `velocity = transform.forward * speed`
   * `radius` as assigned.
2. Clears any previous contents of `prediction`.
3.  If **`bounces == 0`**, simply does one `proj.Predict(...)` from the current position:

    ```csharp
    csharpCopyEditprediction.Add(
        projectileSettings.Predict(
            selfTransform.position,
            null,
            resolution,
            distance,
            collisionLayers,
            triggerInteraction,
            constantAcceleration
        )
    );
    ```
4. If **`bounces > 0`**, runs a loop up to `bounces` times:
   * Calls `proj.Predict(...)` from the current launch point (`pos`) with the current `proj.velocity` and either:
     * `distance` (if `distanceIsTotalLength == false`), or
     * the remaining distance (if `distanceIsTotalLength == true`).
   * Adds the returned `BallisticPath` to `prediction`.
   * If there’s no impact, breaks out (no further bounces).
   * Otherwise, reflects the last‐step velocity against the impact normal and multiplies by `(1 – bounceDamping)`, then uses that as the new `proj.velocity` for the next segment.
   * If `distanceIsTotalLength == true`, subtracts the just‐used segment’s `flightDistance` from remaining distance.

**Designer Usage**

* Call `Predict()` whenever you want to update the visible trajectory (e.g., on aim adjustment or when parameters change).
* After `Predict()`, inspect `prediction` (for example, draw gizmos from each `BallisticPath.steps[i].position`) or feed it directly into a `LineRenderer`/debug draw.

### Shoot

**`void Shoot()`**

Instantiate the `BallisticPathFollow` prefab and assign the precomputed trajectory so the spawned object moves exactly along it.

**Workflow**

1. Instantiates a copy of `template.gameObject` at `transform.position`/`transform.rotation`.
2. Retrieves its `BallisticPathFollow` component (`comp`).
3. Creates a new `BallisticsData` inside `comp` with:
   * `velocity = transform.forward * speed`
   * `radius` as configured.
4. Assigns `comp.path` to a new `List<BallisticPath>(prediction)` (makes a copy).
5. If `prediction` is empty, logs a warning: “No prediction path available, projectile spawned but may not behave as expected.”

**Designer Usage**

* After calling `Predict()`, simply call `Shoot()`. The newly spawned object will begin its path in its next `LateUpdate` call.
* You do not need to manually set `comp.projectile` or `comp.path`—`Shoot()` handles it.

***

## Typical Designer Workflow

1. **Scene Setup**
   * Place a GameObject in the scene (e.g., a “Launcher”) and attach:
     1. `TrickShot`
     2. Any aiming/rotation scripts you want (e.g., rotating to face a target).
   * Assign a `BallisticPathFollow` prefab as `template` on `TrickShot`. Ensure that prefab has a `BallisticPathFollow` component and is configured (layer masks, events, etc.).
2. **Configure Parameters in Inspector**
   * **`speed`**: E.g., `25f` for a medium‐range launch.
   * **`constantAcceleration`**: Leave at `(0, –9.81f, 0)` for earth‐like gravity.
   * **`radius`**: E.g., `0.1f` for a small projectile.
   * **`resolution`**: E.g., `0.02f` for a smooth curve.
   * **`distance`**: E.g., `50f` to trace up to 50 units.
   * **`collisionLayers`**: Tick “Environment” or “Obstacles.”
   * **`bounces`**: E.g., `1` if you want exactly one bounce.
   * **`bounceDamping`**: E.g., `0.3f` to lose 30% speed on each bounce.
   * **`distanceIsTotalLength`**: Enable if you want the sum of all segments capped at `distance` (otherwise each segment is capped individually).
3. **Call `Predict()`**
   *   In a custom aiming script or UI (e.g., when the player adjusts aim), call:

       ```csharp
       csharpCopyEditGetComponent<TrickShot>().Predict();
       ```
   * Use `prediction` to draw a debug arc or a `LineRenderer` so the player sees the full flight + bounce.
4. **Call `Shoot()`**
   *   When the player fires, simply call:

       ```csharp
       csharpCopyEditGetComponent<TrickShot>().Shoot();
       ```
   * A new object (from your `BallisticPathFollow` template) spawns at `transform.position` and immediately begins moving along the precomputed `path`.

***

## Designer Tips & Gotchas

* **Ensure `prediction` Is Up to Date**\
  Always call `Predict()` right before `Shoot()` (or enable `Predict()` in an “OnAimChanged” event). If you forget, `Shoot()` will warn that `prediction` is empty, and the projectile might not travel correctly.
* **Matching Radius & Collider**\
  Use the same `radius` in both `TrickShot` and the `BallisticPathFollow`’s `projectile` so that collisions align perfectly during prediction and actual flight.
* **Distance Logic**
  * If **`distanceIsTotalLength == false`**, each segment can travel up to `distance` before ending—even if the first bounce happened early.
  * If **`true`**, the sum of all segments’ `flightDistance` cannot exceed `distance`, ensuring a hard cap on total arc length.
* **Multiple Bounces**\
  Set `bounces` to the maximum number of bounces you expect. If the path never actually collides before reaching `distance`, the loop breaks early.
* **Performance Consideration**\
  A small `resolution` (e.g., `0.005f`) plus many bounces can generate hundreds of samples—use a slightly larger value (e.g., `0.02f`–`0.05f`) unless you need extreme precision.
* **Custom Gravity**\
  If you want no gravity, set `constantAcceleration = Vector3.zero`. For unusual physics fields (e.g., a planet with weak gravity), adjust accordingly.
