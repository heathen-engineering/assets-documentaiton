# Ballistic Path Line Render

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

`BallisticPathLineRender` visualizes a projectile’s trajectory (including optional bounces) by drawing a line in world space. Designers can configure launch parameters, gravity behavior, collision layers, resolution, and bounce settings directly in the Inspector. Calling `Simulate()` (or enabling `runOnStart`/`continuousRun`) computes the full flight path via the corresponding `BallisticsData.Predict(...)` method and updates a `LineRenderer` to show the arc.

***

## Public Fields & Properties

### **Start**

* **`public Vector3 start`**
  * World-space origin point where the projectile is launched.
  * Designers can set this to a turret’s muzzle, character’s hand, or any desired source.

### Projectile

* **`public BallisticsData projectile`**
  * Reference to a `BallisticsData` asset or component that holds: initial speed, radius, drag, etc.
  * Used internally to call `projectile.Predict(...)` and retrieve a `BallisticPath`.

### **Run On Start**

* **`public bool runOnStart`** (default: `true`)
  * If checked, the component immediately calls `Simulate()` in `Start()`, rendering the path once when the scene begins.

### Continous Run

* **`public bool continuousRun`** (default: `false`)
  * If enabled, `Simulate()` is called every `LateUpdate()`, allowing the line to update in real time as launch parameters change (e.g., moving `start` or adjusting gravity).

### Collision Layers

* **`public LayerMask collisionLayers`** (default: `0`)
  * Specifies which layers to test for collisions when predicting the path.
  * Designers must assign relevant layers (e.g., “Environment”, “Obstacles”) so that the trajectory stops or bounces correctly.

### Trigger Interaction

* **`public QueryTriggerInteraction triggerInteraction`** (default: `UseGlobal`)
  * Controls whether triggers are included in collision checks (e.g., `UseGlobal`, `Ignore`, `Collide`).
  * Adjust if you want the trajectory to stop or bounce off trigger colliders.

### Resolution

* **`[Min(0.001f)] public float resolution`** (default: `0.1f`)
  * The distance increment at which the path is sampled.
    * Lower values (e.g., `0.05f`) yield a smoother, more accurate curve but cost more CPU.
    * Higher values (e.g., `0.2f`–`0.5f`) produce fewer points and can miss short‐range collisions.

### Max Length

* **`public float maxLength`** (default: `10f`)
  * Maximum distance the simulation traces before stopping if no impact occurs.
  * Designers can increase for long‐range arcs or decrease to limit preview length.

### Max Bounces

* **`public int maxBounces`** (default: `0`)
  * Number of times the trajectory should bounce (up to) after its first impact.
  * Each bounce uses a reflected velocity scaled by `(1 – bounceDamping)`.

### Bounce Damping

* **`[Range(0f, 1f)] public float bounceDamping`** (default: `0.2f`)
  * Fraction of velocity lost on each bounce (e.g., `0.2f` means the new speed is 80% of pre‐impact speed).
  * Only used if `maxBounces > 0`. Value must be in `[0, 1]`.

### Gravity Mode

* **`public GravityMode gravityMode`** (enum: `None`, `Physics`, `Custom`; default: `Physics`)
  * Selects how gravity is applied during simulation:
    1. **`None`** – No gravity. The path is a straight line.
    2. **`Physics`** – Uses `Physics.gravity` (typically `(0, –9.81f, 0)`).
    3. **`Custom`** – Uses the vector set in `customGravity`.

### Custom Gravity

* **`public Vector3 customGravity`** (default: `Vector3.zero`)
  * Only used if `gravityMode == GravityMode.Custom`. Defines a custom gravity vector (e.g., `(0, –15f, 0)` for heavier gravity).

***

## Public Methods

### Simulate

* **`public void Simulate()`**
  * Computes a full, sampled trajectory and updates the attached `LineRenderer`.
  * Designer-Visible Behavior:
    1. **Check “Speed”**
       * If `projectile.Speed ≤ 0f`, `Simulate()` returns immediately (nothing to draw).
    2. **Select Gravity**
       * Uses `gravityMode` to pick `Vector3 gravity = Physics.gravity` or `customGravity`, or `Vector3.zero`.
    3. **Clear Previous Data**
       * Empties internal `List<Vector3> trajectory` and `List<RaycastHit> impacts` to avoid stale points.
    4.  **Initial Prediction**

        ```csharp
        csharpCopyEditvar result = projectile.Predict(
            start,              // launch origin
            null,               // no ignore-collider on first segment
            resolution,         // sampling resolution
            maxLength,          // maximum trace length
            collisionLayers,    // layers to hit
            triggerInteraction, // include/exclude triggers
            gravity             // chosen gravity vector
        );
        ```

        * Appends every `step.position` from `result.steps` into `trajectory`.
        * If `result.impact.HasValue`, also stores the `RaycastHit` in `impacts`.
    5. **Handle Bounces (if `maxBounces > 0` and there was an impact)**
       * Computes `remainingLength = maxLength – result.flightDistance`.
       * Copies `projectile` locally (so original asset remains unchanged).
       * Reflects last‐sample velocity about the impact normal (using `Vector3.Reflect`) and multiplies by `(1 – bounceDamping)`.
       * Repeats `Predict(...)` from the impact point, ignoring the now‐hit collider, up to `maxBounces` times or until no further impact.
       * Each subsequent segment’s positions are appended to `trajectory`, and each new impact is added to `impacts`.
       * Deducts each segment’s `flightDistance` from `remainingLength` to cap total drawn length.
    6. **Feed Data to LineRenderer**
       * Ensures an internal buffer (`positionBuffer`) is at least `trajectory.Count` in length; resizes if needed.
       * Copies `trajectory` into `positionBuffer`.
       * Sets `lineRenderer.positionCount = trajectory.Count` and `lineRenderer.SetPositions(positionBuffer)`.
  * **Designer Tips**:
    * Call `Simulate()` explicitly after changing `start`, `projectile`, or any parameters at runtime (unless `continuousRun` is true).
    * Make sure `projectile.Speed` is set properly in your `BallisticsData` asset before calling `Simulate()`.
    * If you want the line to auto-update whenever the camera or launch origin moves (e.g., an aiming reticle), enable `continuousRun = true` and adjust parameters in real time.

***

## Inspector Setup & Typical Usage

1. **Attach to a GameObject**
   * Create an empty GameObject (e.g., “TrajectoryPreview”) in your scene.
   * Add a `LineRenderer` component and configure its material (e.g., a simple unlit color) and width.
   * Add the `BallisticPathLineRender` component to the same GameObject.
2. **Assign Launch & Projectile Data**
   * **`start`**: Drag a Transform (e.g., a turret’s muzzle or player’s hand) from your scene into this field or set a static coordinate.
   * **`projectile`**: Select the `BallisticsData` asset (ScriptableObject) or component that contains the projectile’s initial speed, radius, drag, etc.
3. **Configure Collision & Bounce**
   * **`collisionLayers`**: Tick the layers you want to hit (e.g., “Environment” or “Obstacles”).
   * **`triggerInteraction`**: Choose whether triggers count as hits.
   * **`maxLength`**: Set the maximum trace length in world units (e.g., `50f`).
   * **`maxBounces`**: If you want to preview up to N bounces, set this (e.g., `1` for one bounce).
   * **`bounceDamping`**: Adjust how much speed is lost each bounce (e.g., `0.3f` → 70% retention).
   * **`resolution`**: Lower for finer curves (e.g., `0.05f`), higher for performance (e.g., `0.2f`).
   * **`gravityMode`**:
     * **`Physics`** if you want standard Unity gravity.
     * **`Custom`** if you’re simulating in a non‐Earth environment (e.g., `customGravity = (0, –20f, 0)`).
     * **`None`** for a straight-line preview (e.g., lasers or bullets without drop).
4. **Choose Run Behavior**
   * **`runOnStart`** = **`true`** → Preview appears immediately when you enter Play Mode.
   * **`continuousRun`** = **`true`** → Preview updates every frame (useful for runtime adjusting aim).
   * Otherwise, call `Simulate()` from your script when you want to refresh the trajectory.
5. **Scripting Examples**
   *   **Manual Recalculation (e.g., when player aims):**

       ```csharp
       public class TrajectoryController : MonoBehaviour
       {
           [SerializeField] private BallisticPathLineRender pathPreview;
           [SerializeField] private Transform muzzle;
           [SerializeField] private BallisticsData projectileData;

           void Update()
           {
               // Example: continuously update the start point and re-simulate
               pathPreview.start = muzzle.position;
               pathPreview.projectile = projectileData;
               pathPreview.Simulate();
           }
       }
       ```
   *   **One-Off Preview (e.g., on button press):**

       ```csharp
       public class PreviewOnDemand : MonoBehaviour
       {
           [SerializeField] private BallisticPathLineRender pathPreview;
           [SerializeField] private Transform muzzle;
           [SerializeField] private BallisticsData projectileData;

           void Update()
           {
               if (Input.GetKeyDown(KeyCode.T))
               {
                   pathPreview.start = muzzle.position;
                   pathPreview.projectile = projectileData;
                   pathPreview.Simulate();
               }
           }
       }
       ```

***

## Designer Tips & Gotchas

* **LineRenderer Configuration**
  * Adjust the material and width curve so the path is clearly visible (e.g., a bright color or dashed texture).
* **Performance Considerations**
  * High `resolution` (small steps) + many bounces can generate hundreds of sample points. If updating every frame (`continuousRun`), consider a coarser `resolution` (e.g., `0.2f`–`0.5f`).
  * If you only need a quick preview in the Editor and not at runtime, disable `continuousRun` and run `Simulate()` via a custom Editor script or button.
* **Max Length vs. Bounces**
  * `maxLength` is total distance for **each** segment. Each bounce reduces `remainingLength` by the previous segment’s `flightDistance`. If you want a guaranteed total limit across all bounces, subtract each segment from a master length before calling `Predict(...)`.
* **Trigger Colliders**
  * If you have invisible triggers (e.g., detection zones) in your scene, set `triggerInteraction = Ignore` if you don’t want the path to stop on them.
* **Ensuring Up-to-Date Data**
  * If you change `BallisticsData` (speed/radius) in Play Mode, call `Simulate()` again to reflect those changes. Otherwise, the path will still show the old values.
