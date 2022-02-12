# Ballistics

## Introduction

```csharp
public static class Ballisitics
```

Found in namespace:

```csharp
using HeathenEngineering.PhysKit.API;
```

{% hint style="info" %}
We recommend using aliases to reduce typing and simplify names.



```csharp
using API = HeathenEngineering.PhysKit.API;
```

doing this you can fully qualify the name of this class as

```csharp
API.Ballistics
```
{% endhint %}

This interface uses features derived from Forrest The Woods by Forrest Thomas Smith.\
[https://github.com/forrestthewoods/lib\_fts](https://github.com/forrestthewoods/lib\_fts)

### What can it do?

Used to solve for ballistic (parabolic) trajectory solutions such as throwing a ball, shooting a cannon, etc. The features of this API can be used to find the proper angle to aim at to hit a given target or to find the velocity to launch a projectile at to achieve a desired arc

## Max Range

The first step is typically to determine if the target is within range at all. We can find the max range of a ballistic system with

```csharp
public static float MaxRange(
    float speed, //Speed of the projectile
    float gravity, //The magnitude of gravity (9.8f typically)
    float height) // > 0 hight difference from target
```

## Solution

The main feature of the Ballistics API is the Solution method which comes in several overloads to meet any need.

### Simple Trajectory

```csharp
public static int Solution(
    Vector3 projectile, //The starting position of the projectile
    float speed, //The forward speed of the projectile
    Vector3 target, //The target position to reach
    float gravity, //The magnitude of gravity (9.8f typically)
    out Quaternion lowAngel, // Solution 1
    out Quaternion highAngle) // Solution 2
```

This overload returns an int ranging from 0 to 2 representing the number of valid solutions found. If the value is greater than 1 then there is at least 1 valid solution.

The valid solutions found will be expressed as rotations for a low angle and high angle trajectory.

```csharp
public static int Solution(
    Vector3 projectile, //The starting position of the projectile
    float speed, //The forward speed of the projectile
    Vector3 target, //The target position to reach
    VEctor3 targetVelocity, //Target's velocity
    float gravity, //The magnitude of gravity (9.8f typically)
    out Quaternion lowAngel, // Solution 1
    out Quaternion highAngle) // Solution 2
```

The same as the previous overload only this overload takes a `targetVelocity` and can be used to target a moving object.

### Variable Trajectory

While the above solution are simple we often want to tailor the visuals of a parabolic trajectory such that the angle is not to high or flat and that the projectile has a fixed linear speed as if fired strait at the target. This is the more common solution for simulating say a bow shot where the archer will optimize flight time and range for the target.

```csharp
public static bool Solution(
    Vector3 projectile, //The starting position of the projectile
    float linearSpeed, //Speed of projectile over ground
    Vector3 target, //Target position to reach
    float arcCeiling, //Max hight of the arc to fire on
    out Vector3 firingVelocity, //The speed the projectile should launch at
    out float gravity) //The magnitude of gravity that should be applied to it
```

As with the previous solution there is an overload for targeting a moving target

```csharp

public static bool Solution(
    Vector3 projectile, //The starting position of the projectile
    float linearSpeed, //Speed of projectile over ground
    Vector3 target, //Target position to reach
    Vector3 targetVelocity, //Targets velocity
    float arcCeiling, //Max hight of the arc to fire on
    out Vector3 firingVelocity, //The speed the projectile should launch at
    out float gravity, //The magnitude of gravity that should be applied to it
    out Vector3 impactPoint) //Perdicted impact point 
```

These overloads return a boolean indicating rather or not a solution was found. If a solution was found then the firingVelocity and gravity output parameters will be populated.&#x20;

### Fixed Time

On occasion its important for gameplay that the projectile reach its target at a specific time so we can use the following overload to find the launch velocity. Launch velocity indicates the the direction and speed of the launch.&#x20;

```csharp
public static Vector3 Solution(
    Vector3 projectile, //The starting position of the projectile
    Vector3 target, //The target to reach
    float gravity, //The magnitude of gravity (9.2 typically)
    float flightTime) //The desired flight time
```

This overload outputs a velocity vector. If you need to know the rotation the object should be on you can do&#x20;

```csharp
var rotation = Quaternion.LookRotation(solution) * Vector3.Forward;
```

### Fixed Angle

Some use cases require that you launch the projectile from a given angle and so you need to know what "speed" to launch the projectile at.

```csharp
public static bool Solution(
    Vector3 projectile, //The starting position of the projectile
    Vector3 target, //The target to reach
    float angle, //The launch angle to use
    float gravity, //The magnitude of gravity
    out float speed) //The required launch speed of the projectile
```

## Raycast

The raycast method can be used to trace a ballistic trajectory for a defined length and test for collision along the way. The resulting steps tested will be returned along with the final direction of the projection and any hit data found.

```csharp
public static bool Raycast(
    Vector3 start, //Start point
    Vector3 velocity, //direction and speed
    Vector3 gravity, //full gravity vector
    float resolution, //Distance between steps
    float maxLength, //max length to test along
    LayerMask collsiionLayers, //layers to test for collision on
    out RaycastHit hit, //Hit data if any
    out List<Vector3> path, //points tested 
    out Vector3 direction) //Final look direction of the projectile path
```

This can be used test for collision, draw trajectory arcs, plan for bounces, etc.

## Flight Time

Estimating flight time can be done with the projectiles velocity, the height difference it must travel from start to end and the effect of gravity.

Note that this is an estimate assuming the projectile will travel the full the length of a typical trajectory.

```csharp
public static float FlightTime(
    Vector3 velocity, //The velocity of the projectile 
    float height, //The height the projectile will travel
    float gravity, //The effect of gravity on the projectile
```
