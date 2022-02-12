# 2 Ballistic Ray Casting



{% hint style="success" %}
Available in PhysKit [Complete](https://prf.hn/l/rpoyznk).
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (162) (1).png>)

This scene demonstrates the use of [Ballisitics.Raycast](../../api/ballistics.md#raycast) and the [BallisticsPath](../../components/ballistic-path.md) component to predict the path a thrown object will take including its bounce.

The Ballistic raycast method performs raycasts identifying any points of collision and returning the path that will be followed. The Ballistics Path component uses the path data to draw a line using Unity's built in line renderer that matches this path.

## What do I Learn?

1. How to access the Ballistics API from your scripts
2. How to use Ballistics' Raycast feature
3. How to display a trajectory using the BallisticsPath component.

## Objects

### Trajectory Line

See the DEMO SCRIPTS > Line game object. This uses a Ballistic Path component and a Unity Line Renderer to draw a determined path.

![](<../../../../.gitbook/assets/image (187).png>)

While this component is available for use and will satisfy many simple use cases it also serves as a demonstration on how to use the Ballistics.Raycast method effectively.
