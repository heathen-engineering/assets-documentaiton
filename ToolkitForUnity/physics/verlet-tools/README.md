# Verlet Tools

**Verlet Tools** leverages Verlet integration, a lightweight physics simulation technique ideal for soft-body motion, cloth, hair, tails, and other physics-driven transforms. Named after physicist Loup Verlet, this method calculates motion using position and velocity approximations, without relying on forces, Rigidbody components, or Unity’s FixedUpdate loop.

### Verlet Transform

* Each `VerletTransforms` simulates a transform’s motion using Verlet integration.
* The system is designed for stable, springy motion with low performance cost.
* Parameters such as drag, damping, elasticity, and stiffness are controlled via artist-friendly animation curves.
* Fully decoupled from Unity physics, it works on arbitrary Transform hierarchies, making it perfect for stylised secondary animation, procedural motion, and non-physical entities.

### Verlet Line

In addition to transform-based animation, Verlet Tools include **Verlet Line**, a powerful system for simulating ropes, cables, chains, and similar line-based objects.

Key features of Verlet Line include:

* **Full collision support** along the entire length of the line, allowing realistic interaction with world geometry.
* **Pinning system** with three modes:
  * _Static_: pins a line point rigidly in world space.
  * _Kinematic_: pins an object to follow a line, point’s position and rotation.
  * _Force Transfer_: connects the line with Rigidbody physics, enabling forces to flow bidirectionally (e.g., ropes dragging objects or cranes lifting loads).
* Adjustable **resolution** for tuning simulation detail and performance.
* **Custom mesh support** for the line’s profile and caps, allowing full control over visual appearance.
* Per-node parameter control via curves, enabling fine-tuning of properties like mass, damping, and stretchiness along the rope.
* Designer-friendly tools for editing control points and pins directly in the Unity Editor.

Together, Verlet Transform and Verlet Line provide a flexible, performant, and artist-friendly toolkit for physics-driven animation and simulation in Unity, enabling rich, dynamic behaviours without the overhead or complexity of traditional rigidbody physics.
