# Ballistic Trajectory

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Ballistic trajectory some times referred to a parabolic trajectory is the path a body takes while launched at a particular angle. This accounts for the drop rate applied by gravity, the launch angle and speed of the projectile.

{% embed url="https://www.youtube.com/watch?v=oQ-OaVW191k" %}

Ballistic trajectories are usually applied with relatively slow moving or very long ranged projectiles where the player can see and "feel" the "lob" of the projectile be that a basketball thrown down court, an arrow shot at a target or a grenade bounced off a wall into a room or even an artillery round fired from miles away.

The [Ballistic API](../../api/ballistics.md) provides you with efficient, easy to use and stable tools for calculating ballistic solutions so your projectiles can remain active physically simulated objects but follow a predictable ballistic trajectory.

## Use Cases

### Fantasy Trajectory

Finding the solution to a trajectory with fixed parameters such as known gravity, projectile velocity, etc. is rather simple however its results are less interesting visually in that the resulting arc of the trajectory will only be that nice middle height arc at the extents of the range of the projectile.

That is you will be firing with a very high arc or a very flat arch to hit nearby targets and that doesn't usually suit our art directors needs.

Our [Ballistic API ](../../api/ballistics.md#fixed-time)has a solution, tell us where the target is, how fast you want the projectile to get there and how high you want that arc. We will provide the required gravity and velocity of the projectile to produce the ideal arc with a physically simulated projectile.

### Hitting a moving target

Hitting a moving target with simple direct flight path is relatively simple ... and something our Maths API helps you with. Hitting a moving target with a physically simulated trajectory is much harder as the change in flight time can be difficult to predict.

Our Ballistics API provide solutions for 3 different approaches. Rather your going for a fantasy style arc or using a constant gravity we can help you lead your target predict flight paths and impact points over time.
