# Ballistics Tools

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Ballistic trajectory some times referred to a parabolic trajectory is the path a body takes while launched at a particular angle. This accounts for the drop rate applied by gravity and optionally other constant forces, the launch angle and speed of the projectile are also applied resulting in a curved or arced trajectory.

{% embed url="https://www.youtube.com/watch?v=V8n8joZ8aTw" %}

{% embed url="https://www.youtube.com/watch?v=oQ-OaVW191k" %}

Ballistic trajectories are usually applied with relatively slow moving or very long ranged projectiles where the player can see and "feel" the "lob" of the projectile be that a basketball thrown down court, an arrow shot at a target or a grenade bounced off a wall into a room or even an artillery round fired from miles away.

The [Ballistic API](../api/ballistics.md) provides you with efficient, easy to use and stable tools for calculating ballistic solutions so your projectiles can remain active physically simulated objects but follow a predictable ballistic trajectory.

## Use Cases

### Deterministic Trajectory

When you need to know the flight path, it's bounces and have the projectile actually do what you perdicted reliably.

Our Trick Shot component, avaiolable for both 2D and 3D can "raycast" a trajectory, pre-determine the bounces and yield a path that gives a physically accurate path that a projectile can be made to follow.

Rather you are creating a Peggle-like puzzle game or throwing grenades or maybe a golf simulator the Trick Shot component makes this a nearly code-free task.

### Fantasy Trajectory

Finding the solution to a trajectory with fixed parameters such as known gravity, projectile velocity, etc. is rather simple however its results are less interesting visually in that the resulting arc of the trajectory will only be that nice middle height arc at the extents of the range of the projectile.

That is you will be firing with a very high arc or a very flat arch to hit nearby targets and that doesn't usually suit our art directors needs.

Our [Ballistic API ](../api/ballistics.md#fixed-time)has a solution, tell us where the target is, how fast you want the projectile to get there and how high you want that arc. We will provide the required gravity and velocity of the projectile to produce the ideal arc with a physically simulated projectile.

Fantasy Trajectory lets you tailor the look and feel of the projectiles flight to suit cinematic or gameplay needs while still being physically active and perdictable.

### Hitting a moving target

Hitting a moving target with simple direct flight path is relatively simple ... and something our Maths API helps you with. Hitting a moving target with a physically simulated trajectory is much harder as the change in flight time can be difficult to predict depending on the effects the projectile expereinces.

Our Ballistics API provides solutions for 3 different approaches. Rather your going for a fantasy style arc or using a constant gravity we can help you lead your target and predict flight paths and impact points over time.
