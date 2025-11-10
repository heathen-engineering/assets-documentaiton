# Ballistics

**Ballistics** is a compact, ready-to-use toolkit for realistic projectile behavior in Unity. Whether you’re building turrets, grenades, arrows, or any “lob-and-hit” mechanic, these components and utilities let you skip the tedious math and focus on gameplay.

* **Instant Aiming Solutions**\
  • **BallisticAim** calculates low- and high-arc rotations for a two-pivot launcher (e.g., turret or cannon), given muzzle speed and gravity (or custom acceleration). It even handles moving targets with leading.\
  • **BallisticTargeting** wraps BallisticAim, exposing a simple `HasSolution` flag—ideal for UI or “lock-on” indicators.
* **Full-Flight Trajectory Data**\
  • **BallisticsData** holds your projectile’s velocity and radius, plus helper properties (`Speed`, `Direction`, `Rotation`). One call to `Predict(...)` returns a complete **BallisticPath** (sampled positions, velocities, timestamps, and collision info).\
  • **BallisticPath** itself stores every `(position, velocity, time)` step, flight distance/time, and impact details. Its `Lerp(time)` method interpolates anywhere along the arc for effects or debugging.
* **Visualization Tools**\
  • **BallisticPathLineRender** draws a live 3D trajectory (including optional bounces) with a LineRenderer. Simply assign a BallisticsData asset, set resolution, gravity, bounces, and collision layers—and watch the arc appear.\
  • **TrickShotLine** reads from **TrickShot**’s predicted paths and updates a LineRenderer every frame—perfect for “aim-and-fire” previews.
* **Runtime Path Following**\
  • **BallisticPathFollow** takes one or more `BallisticPath` segments and moves any GameObject along that exact sample sequence, including simulated “planned” collision callbacks. When the path ends, it can hand off to Unity physics with the final velocity.\
  • **TrickShot** combines prediction and runtime behavior: call `Predict()` to build multi-bounce paths, then `Shoot()` to spawn a BallisticPathFollow prefab that follows your precomputed trajectory automatically.
* **Under-the-Hood Math Library**\
  The static **Ballistics** class provides over 30 methods for any projectile problem:\
  • **MaxRange** / **FlightTime** / **FinalVelocity** calculations (2D and 3D).\
  • **Solution** overloads for low- and high-arc aiming at stationary or moving targets (including “arc-ceiling” and “fixed-time” variants).\
  • **Speed-Given-Angle** solvers, plus step-by-step **Raycast** and **SphereCast** routines to sample full flight paths or detect impacts along the way.

All scripts are designer-friendly (drag-drop in the Inspector) and lightweight, with adjustable sampling resolution and layer masks. You get both 2D and 3D versions, custom gravity support, bounce handling, and built-in collision callbacks—everything you need to build accurate, visually clear projectile mechanics without reinventing the wheel.
