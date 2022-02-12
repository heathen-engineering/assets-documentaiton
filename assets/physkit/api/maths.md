# Maths

## Introduction

```csharp
public static class Maths
```

Found in namespace:

```csharp
using HeathenEngineering.PhysKit.API;
```

{% hint style="info" %}
We recommend using aliases to reduce typing and simplify names. and reduce possible collisions with similarly named objects.



```csharp
using API = HeathenEngineering.PhysKit.API;
```

doing this you can fully qualify the name of this class as

```csharp
API.Maths
```
{% endhint %}

### What can it do?

A lot, the maths API is our home for all those formula and calculations that have a lot of use but don't fit nicely into a single API rather that's because they fit into many or that they are simply unique little gems worthy of sharing but not sufficient for a full API.

## Intercept

A number of intercept formulas have been provided which can be used to calculate point in space where an interception will occur between two moving objects ... if any.

### Fast Intercept

A simple fast formula suitable for situations where you know there is a solution. For example you know that if a subject is faster than its target there is some solution however this method doesn't handle the case where there simply is no solution such as the target moving faster than the subject.

```csharp
var point = Maths.FastIntercept(start, speed, targetBody);
```

or

```csharp
var point = Maths.FastIntercept(start, speed, targetPos, targetVelocity);
```

or

```csharp
var point = Maths.FastIntercept(start, speed, targetPos, targetHeading, targetSpeed);
```

### Safe Intercept

The same options are available as a Safe Intercept which will return a nullable point. These variations test for solution and return a null result if none is found e.g.

```csharp
var point = Maths.SafeIntercept(...);
if(point.HasValue)
    //Solution found
else
    //No solution
```

### Intercept Time

This calculates the amount of time to intercept a target ... this assumes of course there is a solution and will return 0 if there is no solution.

```csharp
var time = Maths.InterceptTime(speed, localPosition, closingVelocity); 
```

Example use

```csharp
var localPosition = targetSubject.position - position;
var closingVelocity = targetSubject.velocity - ((position - targetSubject.position).normalized * speed);

var time = InterceptTime(speed, localPosition, closingVelocity);

if(time > 0)
    //Solution found
```

## Transform Formulas

These are formulas that help us work with rigidbodies and transforms, things like finding the amount of torque we need to apply to rotate to a specific facing direction or the force needed to reach a given velocity.

### Quadratic Drag

{% hint style="info" %}
Tip

Don't be overly obsessed with "Realistic" even in a simulator game "real" is a very flexible term and for good reason; its hard to do and in many cases impossible to achieve with current technology ... even where we can get very close to real ... reality is not as much fun as fiction in most cases.



Use the "real" values you google up as a good starting point but don't hesitate to tweak them to get the desired results.
{% endhint %}

put simply the drag effect on a body is proportional to the equar of its speed and the density of the volume its moving through. This is why it takes much less energy to go form say 0 to 5 meters per second than it does to go from 5 to 10 meters per second.&#x20;

This is important in games where we for example want to simulate racing, the rate of acceleration of a car or boat should slope off the faster it goes until that change is 0 and the vehicle has reached its maximum speed. One of many ways to simulate this is to approximate the drag effect.

```csharp
var drag = Maths.QuadraticDrag(coefficent, density, speed, crossSectionArea);
```

... So what do all those parameters mean?

**Coefficent**\
The Coefficent or "Drag Coefficent" is a "magic number" usually determined through experimentation that accounts for numerous factors impacting drag including the surface, shape, etc. You can find drag coefficents for various real world shapes and objects with a simple google search and then adjust off that to achieve your desired effect.

**Density**\
Density, this refers to the density of the volume that is apply drag to you. Again a quick google search will pull back the density values for various substances ... two commonly used ones

15 centigrade air at sea level = 1.225 kg/m^3\
Water = 997 kg/m^3 or 1000 kg/m^3 depending on the paper you read

**Speed**\
Speed is the magnitude of your velocity

**CrossSectionArea**\
The cross section is basically the silhouette as it would appear if you where looking head on into that moving object.

### Force to reach

We have provided you with quick functions to estimate the force or torque required to reach a given state on a given rigidbody.

```csharp
Maths.ForceToReachLinearVelocity(body, targetVelocity);
```

```csharp
Maths.ForceToReachAngularVelocity(body, targetVelocity);
```

```csharp
Maths.TorqueToReachDirection(body, targetDirection);
```

```csharp
Maths.TorqueToReachRotation(body, targetRotaiton);
```

### Lerp To

The lerp feature in Unity's math tools is great but a bit limited when you need to maintain a fixed speed. Our LerpTo methods will move a vector or rotate a quaternion toward a target at a given speed.

For a linear transform this basically the same as Lerping where t = deltaTime \* speed but respects final distance.

```csharp
Maths.LerpTo(from, to, speed, timeStep);
```

This works for Vector3 positions and Quaternion rotations. When used with Rigidbody this will return the Force To Reach the target position or rotation over that time. e.g. the acceleration force to be applied.

### Rotate Around

A simple tool to rotate a vector around another given a eular or quaternion similar to Transform's Rotate Around only doesn't require a transform.

```csharp
Maths.RotatePointAroundPivot(point, pivot, angle)
```

or

```csharp
Maths.RotatePointAroundPivot(point, pivot, rotation);
```

### Get Direction

{% hint style="info" %}
Unity already provides these however they are asked for all the time so we have documented it, added it to our API and commented it in code.
{% endhint %}

Simple methods for converting a quaternion rotation into a direction vector. We found this was asked for a lot and fellow math geeks tend to spend a lot of time explaining that a quaternion doesn't have a direction ... which is true ... but we all know full good and well that what you mean when you ask us how to convert a quaternion into a direction is

If my rotation was identity (standing up looking forward) and I rotated the amount of that rotation ... what would my (Forward, Left, Up, etc.) be.

Well here you go

```csharp
var forward = Maths.GetForwardDirection(rotation);
var back = Maths.GetBackDirection(rotation);
var up = Maths.GetUpDirection(rotation);
var down = Maths.GetDownDirection(rotation);
var right = Maths.GetRightDirection(rotation);
var left = Maths.GetLeftDirection(rotation);
```

And the inverse ... to get a rotation from a direction ... again we understand this question to mean what would the look rotation be if I was to look from identity to that world direction.



## Misc

A few more features that don't fit well into a grouping

### Nearest Point on Line

You can find the nearest point on a ray (line with infinite length) or a segment (finite line)

```csharp
var point = Maths.NearestPointOnLineSegment(start, end, subject);
```

or

```csharp
var point = Maths.NearestPointOnLine(start, direction, subject);
```

### Fall Distance

How far would I fall over X time?

```csharp
var distance = Maths.FallDistance(gravityStrength, fallTime);
```
