# Ballistic Trajectory

{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

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
