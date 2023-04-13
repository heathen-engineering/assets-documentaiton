# (3D) Deterministic Bounce Prediction

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="1-buoyancy-example.md">Buoyancy</a></td><td><a href="1-force-effect-fields.md">Force Effects</a></td><td><a href="2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

This scene demonstrates the use of [Trick Shot](../components/trick-shot.md) and the [Trick Shot Line](../components/trick-shot-line.md) component to predict the path a thrown object and will take into account bounces.

The tool can be used to quickly and easily fire physically simulated projectiles from throwing a ball or grenade to shooting arrows, firing cannons and more. The Trick Shot tool handles all the calculations for you including launching the projectile via the "[Shoot](../components/trick-shot.md#shoot)" method.

The projectile launched by [Trick Shot](../components/trick-shot.md) uses the [Ballistic Path Follow](../components/ballistic-path-follow.md) component which allows the projectile to accurately follow the pre-planned path and to optionally react to changes in the environment as required.

## What do I Learn?

1. How to use [Trick Shot](../components/trick-shot.md) to plan and execute shots
2. How to use [Ballistic Path Follow](../components/ballistic-path-follow.md) to manage projectiles
3. How to display a trajectory using the [Trick Shot Line](../components/trick-shot-line.md) component.

## Objects

## Emitter GameObject

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

The emitter game object does all the real work in the sample scene and houses the Trick Shot component and the Trick Shot Line component. These do the work of calculating the path and displaying it. A simple call to Shoot then causes the Trick Shot component to launch a projectile which will obey the path.

### [Trick Shot](../components/trick-shot.md)

The trick shot component is used to predict a trajectory and "shoot" a projectile that will obey that planned path e.g. a Ballistic Path Follow projectile. This allows for accurate deterministic prediction of bounces and collisions, the ability to handle unexpected (dynamic) collisions and changes to the environment.

### [Trick Shot Line](../components/trick-shot-line.md)

The trick shot line component is used to control the Line Renderer and draw the resulting path. It simply reads the prediction from the Trick Shot component and updates the points displayed by the Line Renderer.

## Sphere GameObject

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

A simple stand in for our projectile which uses the Ballistic Path Follow component to track the planned path.
