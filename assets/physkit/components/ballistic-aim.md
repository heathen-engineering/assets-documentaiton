# Ballistic Aim

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (600).png" alt=""><figcaption></figcaption></figure>

## Introduction

<figure><img src="../../../.gitbook/assets/image (621).png" alt=""><figcaption></figcaption></figure>

And easy to use solution for code free management of turrets. Add this to a game object and configure the "Y" (left and right rotation) and the "X" (up and down rotation) pivot and limits and we will do the rest. You can simply call "Aim" and we will track the target if a projectile solution available.

## Fields and Attributes

### Initial Velocity

```csharp
public float initialVelocity;
```

The speed of the projectile when it is fired / shot.

### Y Pivot

```csharp
private Transform yPivot;
```

The transform to be rotated when calculating the "left and right" angle to aim down.

### X Pivot

```csharp
private Transform xPivot;
```

The transform to be rotated when calculating the "up and down" angle to aim down.

### Y Limit

```csharp
public Vector2 yLimit;
```

The x value of this vector is the minimal angle the Y Pivot will be allowed to assume and the y value is the maximum angle the Y Pivot will be allowed to assume. use x =-180 and y = 180 to enable free movement.

### X Limit

```csharp
public Vector2 xLimit;
```

The x value of this vector is the minimal angle the X Pivot will be allowed to assume and the y value is the maximum angle the X Pivot will be allowed to assume. use x = -180 and y = 180 to enable free movement.

## Methods

### Aim

Call this method to update cause the tool to rotate the Y and X Pivot to aim at the indicated target.

```csharp
public bool Aim(Vector3 target);
```

or

```csharp
public bool Aim(Vector3 target, Vector3 targetVelocity);
```

You can specify a static point to aim at or indicate the current position and velocity to have the system estimate and intercept trajectory.

If this method returns false it indicates that no valid solution could be found, this happens if the pivot limits where hit or if the object is simply out of range given the initial velocity you configured.
