# 1 Verlet Spring Simple Transforms

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

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
