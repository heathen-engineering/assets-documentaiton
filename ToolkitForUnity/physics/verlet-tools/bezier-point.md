# Bezier Point

Represents a single cubic Bézier control point, including its position and handle vectors. This structure is fundamental for defining smooth curves using Bézier splines.

A `BezierPoint` defines:

* A spatial point (`position`)
* An incoming handle (`handleIn`)
* An outgoing handle (`handleOut`)

These components collectively allow for precise control of curvature and continuity between connected Bézier segments.

***

## Structure

```csharp
[Serializable]
public struct BezierPoint
{
    public float3 position;
    public float3 handleIn;
    public float3 handleOut;
}
```

***

## Fields

### Position

* **Type:** `float3`
* **Description:** The main coordinate of the control point in space. This is the anchor point of the curve segment.

### Handle In

* **Type:** `float3`
* **Description:** The incoming control handle, defined relative to `position`. Controls the curvature of the curve segment approaching this point.

### Handle Out

* **Type:** `float3`
* **Description:** The outgoing control handle, defined relative to `position`. Controls the curvature of the curve segment leaving this point.

***

## Usage

Used in cubic Bézier curve implementations where each segment is defined by:

* A start point (`position`)
* A start tangent (`handleOut`)
* An end tangent (`handleIn`)
* An end point (next `BezierPoint.position`)

This allows for intuitive curve editing and consistent spline behavior.

```csharp
csharpCopyEditBezierPoint point = new BezierPoint
{
    position = new float3(0, 0, 0),
    handleIn = new float3(-1, 0, 0),
    handleOut = new float3(1, 0, 0)
};
```

In this example, the point sits at the origin with symmetrical tangents extending in the X-axis direction.
