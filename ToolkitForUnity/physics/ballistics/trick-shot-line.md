# Trick Shot Line

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

TrickShotLine and TrickShotLine2D have the same funcitonlity just different simulation space: `TrickShotLine` renders a visual preview (using a `LineRenderer`) of the multi‐bounce trajectory computed by a sibling `TrickShot` component. It concatenates all sampled points from each `BallisticPath` in `trickShot.prediction` and feeds them to the `LineRenderer`. Designers can choose to run the prediction once at startup or continuously update it every frame.

***

## Requirements

* **`[RequireComponent(typeof(LineRenderer))]`**
* **`[RequireComponent(typeof(TrickShot))]`**\
  Ensure this GameObject has both a `LineRenderer` (for drawing the path) and a `TrickShot` (for computing the trajectory).

***

## Public Fields

### Run on Start

* **`public bool runOnStart`** (default: `true`)
  * If checked, `trickShot.Predict()` is called once in `Start()` (before the first frame).
  * Use this when you only need a static preview that doesn’t change after the scene begins.

### Continuous Run

* **`public bool continuousRun`** (default: `true`)
  * If checked, `trickShot.Predict()` is called every `LateUpdate()`, and the line is updated each frame.
  * Use this for real‐time previews (e.g., aiming UI that follows the cursor or moving launcher).

***

## Typical Designer Workflow

1. **Scene Setup**
   * Create (or use) a launcher GameObject and attach:
     1. `TrickShot` (configured with speed, bounces, etc.)
     2. `TrickShotLine`
   * Add a `LineRenderer` component alongside. Configure its material and width so it’s clearly visible.
2. **Inspector Configuration**
   * **`runOnStart`**:
     * **`true`** → Preview is generated once when the scene starts. If your launcher and gravity are static at startup, leave this checked.
     * **`false`** → No prediction at start; you’ll call `TrickShot.Predict()` manually or let `continuousRun` handle it.
   * **`continuousRun`**:
     * **`true`** → The line updates every frame. Good for dynamic aiming or moving launchers.
     * **`false`** → The line only appears once (if `runOnStart` is `true`) or after you manually call `TrickShot.Predict()` in your script.
3. **Runtime Behavior**
   * If **`runOnStart = true && continuousRun = false`**:
     * At `Start()`, the trajectory is computed once, and the line is drawn. It remains static thereafter.
   * If **`continuousRun = true`**:
     * Each `LateUpdate()`, `TrickShot.Predict()` recomputes `prediction` (sampling new points based on current position, rotation, etc.).
     * `UpdateLine()` then refreshes the `LineRenderer` to reflect any changes (e.g., new aim direction).
4. **Manual Triggering**
   *   If both fields are **`false`**, no prediction occurs automatically. To draw the line:

       ```csharp
       csharpCopyEditvar ts = GetComponent<TrickShot>();
       ts.Predict();
       GetComponent<TrickShotLine>().UpdateLine(); // though UpdateLine() is private, you can toggle continuousRun or call Predict + wait one frame
       ```
   * The simplest approach is to set `runOnStart = false, continuousRun = false`, then call `Predict()` in your custom script and rely on `LateUpdate()` of `TrickShotLine` during the next frame to draw it.

***

## Designer Tips & Gotchas

* **LineRenderer Setup**
  * Ensure the `LineRenderer`’s “Use World Space” is checked. This script sets it automatically, but double‐check the material, color gradient, and width curve to suit your scene.
  * If the line appears too thin or invisible, increase the `startWidth`/`endWidth` and assign a bright or unlit material.
* **Minimizing Garbage**
  * `UpdateLine()` calls `trajectory.ToArray()` each frame, which allocates a new array. If you experience GC spikes, consider caching a larger buffer or switching to a pooled array approach. In most scenes, this is negligible.
* **Matching Prediction to Projectile**
  * Make sure your `TrickShot` parameters (speed, resolution, bounces, etc.) match your actual projectile’s behavior. The line will only be accurate if those values reflect the real‐time launch settings.
* **Performance Considerations**
  * High sampling resolutions (small `resolution` in `TrickShot`) and many bounces can produce thousands of points. If `continuousRun = true`, this can affect frame rate.
  * If you only need a static preview, set **`runOnStart = true`** and **`continuousRun = false`** to avoid recomputing unnecessarily.
* **Empty or Null Paths**
  * If `trickShot.prediction` contains no valid paths (e.g., `Predict()` was never called or the target is out of range), `trajectory.Count` will be zero and the line will not draw.
  * You can check in `TrickShot` or your own script whether `prediction` is empty before displaying UI elements.
