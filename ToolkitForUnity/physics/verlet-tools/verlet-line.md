# Verlet Line

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

A MonoBehaviour component for creating and simulating a 3D line, such as a rope, cable, ribbon, etc. The tool can create a rope mesh based on its own generated components, or you can optionally provide it with Start Cap, Profile and End Cap values.

## Editor Controls

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

In the Scene view, you can toggle a series of spheres displayed along the length of the line. These spheres are scaled based on the taper settings and provide a visual guide to the size and placement of the final line. Use the checkbox to turn this visualisation on or off, and adjust the sphere colour to your preference.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

**Control Points Editing**\
When you select the GameObject, gizmo handles appear on each control point, allowing you to edit the line directly. You can add control points through the Control Points foldout — clicking the "+" button inserts a new point either halfway between this and the next point or, if it’s the last point, one meter forward from it.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

## Settings

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

You can define your settings either as a ScriptableObject—allowing you to configure once and reuse across multiple lines—or set them directly on the component. To create a ScriptableObject, right-click in your Assets folder and choose **Create > Variable > Verlet Line Settings**. Both approaches provide the same configurable options.

### Taper

Defines the scale along the length of the line, similar to taper controls in 3D modeling tools like Blender. The float value sets the base scale in Unity units (e.g., 0.05 equals 5 cm). The accompanying curve controls how this scale is distributed, allowing the line to grow or shrink along its length.

### Constant Acceleration

Applies a uniform force to all points along the line, commonly used to simulate gravity. It can also represent other constant forces, like centripetal force. This is useful for simulating effects such as a hanging object inside a moving container that isn’t actually moving in the scene.

### Mass

Represents the virtual mass of the rope used when applying impulses during collisions between the rope and other objects. Like **Taper**, it includes a curve to control how the mass is distributed along the length of the line.

### Damping

Scaled damping applied as a factor of velocity to soften movement along the line. Includes a curve to control how damping is distributed from start to end.

### Stretchiness

Controls how much a segment can stretch beyond its rest length. A value of 0 means no stretch (max length = rest length), while 1 allows up to 200% stretch. Includes a curve to adjust stretch distribution along the line.

> **Note:** If two pins exist on either side of a segment (e.g., at 0.25 and 0.75), the segment between them can stretch infinitely because the pins override stretch constraints. However, segments beyond the outer pins (e.g., from 0 to 0.25 and 0.75 to 1) are limited by the stretchiness value.

> **Future Note:** When _Tensile Strength_ and _breaking_ are implemented, stretchiness will affect the breaking behavior. Forces will only be considered once the segment has stretched beyond its maximum length defined by stretchiness, acting as a threshold before applying break forces.

### Enable Collision & Collision Layers

Enabling collision will test for contacts at each control point, allowing the rope to naturally drape and interact with objects in the scene. The _Collision Layers_ field lets you specify which Unity collision layers the rope should consider for collisions, giving you control over what it does and doesn’t collide with.

### Tensile Strength

_Not implemented yet._ This will eventually define the force limit at which the rope breaks. Like _Taper_, it includes a curve to control how the strength is distributed along the length of the line.

### Constraint Iterations

This setting is on the script itself and must be configured per line. It controls how many times the constraints are resolved per update, effectively “tightening” the simulation. More iterations reduce springiness but increase CPU usage. The value is clamped between 1 and 32 by default.\
Resolution and Iterations are the primary tools for tuning rope behavior: generally, a higher Resolution value (meaning fewer simulation points) combined with more Iterations yields a tighter, more accurate line.

## Pins

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Pins let you attach specific points along the line to other transforms in different ways:

* **Static Pin:** Think of this as nailing the rope to a fixed point. The pinned point on the rope won’t move from that transform point (the transform can move and the rope point will follow), while the rest of the rope behaves normally. You can have multiple static pins, but only one per point.
* **Kinematic Pin:** The opposite of Static. The object you pin will follow the line’s point precisely, including its rotation, as if it’s part of the line itself.
* **Force Transfer Pin:** This uses Unity Physics and requires a Rigidbody on the pinned object. Forces are exchanged between the line and the Rigidbody, allowing interactions like dragging a box across the ground or lifting heavy loads with a crane.

### Mode

Select the type of pin behavior: Static, Kinematic, or Force Transfer, as described above.

### Transform

The position and rotation linked to the specified "Line Position." This represents where the rope is attached or what is attached to the rope.

### Line Position

A normalized value from 0 to 1 representing the location along the length of the line, from start to end. The actual pin attaches to the closest simulation point near this position.

### Force Target

Shown only for Force Transfer pins, this is the Rigidbody that the line will apply forces to and receive forces from.

### Force Scale

This acts like a "virtual mass" scaling the forces exchanged between the line and the Rigidbody. Typically, a value around 100 times the Rigidbody’s mass works well for a sturdy lift. Setting this too high can cause erratic behavior, while too low a value makes the rope feel stretchy relative to the body’s movement.

### Snap Point

This defines the point at which the line will snap. If the scale of this value is < 0 then the feature is disabled. If the value is >=0 the value represents how far past "resting length" a segment can stretch before it breaks.

Example: With a value 0.5, the segment can stretch 50% beyond its resting length. If the resting length is 0.1 then it will break at 0.15

### On Break (event)&#x20;

This event is tied to Tensile Strength and is not yet implemented. It will be triggered when a pin’s force limit is exceeded and the connection breaks.

## Mesh Generation

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Distance Between Segments

Previously refered to as "Resolution"

This defines the spacing between each simulation segment along the line, measured in Unity units (1 unit = 1 meter). For example, a value of `0.075` means each segment is 7.5 cm apart.

Distance Between Segments directly affects both the simulation’s fidelity and performance. A **lower** resolution (smaller number) results in more points, making the line more **flexible and responsive**, but also more **springy** or unstable unless you increase Constraint Iterations. A **higher** resolution (larger number) reduces the number of simulation points, leading to a **firmer**, less stretchy line with lower performance cost.

> For most use cases, a value around **0.1** (10 cm) works well.\
> If the rope needs to bend sharply (e.g. wrapping tightly around objects), values as low as **0.05** (5 cm) may be more appropriate.

**Important:** _More is not always better._ If you want the rope to feel firm, stopping rather than stretching — aim for the **highest resolution value** you can use that still meets your visual and movement needs. Fewer simulation points means a more solid-feeling line and better performance.

### Mesh

If no mesh is provided, the system will auto-generate one using a hemisphere for the start and end caps, and a simple ring (loop of vertices) as the profile.

If you choose to provide a custom mesh, it should be **oriented facing the +Z axis**.

* For example, a conical start/end cap should have its **point facing +Z**, with the **base centred at (0, 0, 0)**.
* The profile mesh should be a **loop of vertices lying flat on the XY plane**, forming a ring shape around the origin.

This orientation ensures the mesh is correctly aligned and deformed along the line during simulation.

### Material

If no material is assigned, the default material for your current render pipeline will be used.\
The generated mesh uses separate materials for the caps and the main body (profile) of the line, allowing for independent styling of each part.

### Scale

The scale factor needed to make the provided mesh match Unity’s unit size.\
For example, if your profile loop has a diameter of 0.1 meters, set the scale to 10 so it’s treated as 1 unit in the system.

