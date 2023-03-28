# 1 Verlet Spring Simple Transforms

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="1-ballistic-basics.md">Ballistics</a></td><td><a href="1-buoyancy-example.md">Buoyancy</a></td><td><a href="1-force-effect-fields.md">Force Effects</a></td><td><a href="2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../../.gitbook/assets/Verlet Trans.png>)

This scene demonstrates the use of Verlet Spring on simple transform hierarchies. You will find a tower structure with a chain of transforms being rotated like a whip. This tower interacts with fixed objects demonstrating collision. In addition you will find a field of Verlet Springs also simulating collision with a ball that will follow the mouse on the plane.

## What do I Learn?

1. Using [Verlet Spring](../../components/verlet-spring.md) as a general use Physics joint
2. Setting up Verlet Spring components with constant configuration (the tower)
3. Setting up Verlet Spring components with [referenced configuraiton](../../objects/verlet-hierarchy-settings.md) (the grass)
4. Verlet Spring collision simulation

## Objects

### Tower

The tower object's pivot child implements the Verlet Spring component and a Constant Angular Velocity component. The Verlet Spring has a single configured hierarchy configured with a constant configuration ... this means the configuration is defined as part of the game object its self.

The tower Verlet Spring rotates around whipping across the meshes in its path demonstrating a rope or chain simulation as well as complex collision detection.

### Grass Blades

This is a collection of just under 300 Verlet Spring objects all set to sample collision. This demonstrates fixed Verlet Springs responding to moving objects. The Grass Blades are all using a [Verlet Hierarchy Settings](../../objects/verlet-hierarchy-settings.md) object meaning you can change a value in one spot to effect all 280+ objects.

### Ball Pivot

This is a simple sphere with a basic sample script causing it to move to the mouse position on the plane rendered in the scene, you can use this ball to introduce collision to the grass blades or the whip if you can manage to catch it.
