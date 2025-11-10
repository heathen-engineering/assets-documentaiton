# Scaled Animation Curve

`ScaledAnimationCurve` is a utility class that pairs a standard Unity `AnimationCurve` with a `scale` factor. This allows the designer to create curves that represent relative influence (e.g., drag, damping, stiffness) while retaining precise control over their magnitude via scaling.

This type is commonly used in simulation parameters within the **Verlet Physics Transform** system to modulate forces and responses over a normalised input space (e.g., `0–1 weight`).

In Unity, `AnimationCurve` is a powerful way to represent changes over time or across a value range. However, when using these curves as part of physical or procedural systems, it’s often useful to apply a consistent multiplier across all outputs — for tuning or balancing purposes.

`ScaledAnimationCurve` provides this ability and integrates cleanly with the Unity Inspector through a custom drawer.

***

## Fields

### Scale

* `public float scale`
  * A multiplier applied to the evaluated result of the curve.

### Curve

* `public AnimationCurve curve`
  * The Unity animation curve used for interpolation.

***

## Methods

### Evaluate

#### `Evaluate(float weight)`

Returns the value of the curve at `weight`, scaled by `scale`.

```csharp
float result = scaledCurve.Evaluate(0.5f);
```

***

### Linear

#### `Linear(...)`

Creates a linear `ScaledAnimationCurve` between two points.

```csharp
var curve = ScaledAnimationCurve.Linear(1f, 0f, 0f, 1f, 1f);
```

***

### EaseInOut

#### `EaseInOut(...)`

Creates an ease-in-out `ScaledAnimationCurve` between two points.

```csharp
var curve = ScaledAnimationCurve.EaseInOut(1f, 0f, 0f, 1f, 1f);
```

***

## Inspector Support

A custom property drawer is provided for the Unity Editor, allowing the `scale` and `curve` to be edited side-by-side in a compact form.

This makes it easy to tune both the curve shape and the magnitude directly in the inspector without needing to create additional tooling.

***

## Use Case Example

Used in `VerletTransformTreeSettings` to modulate behaviour of a physics chain:

```csharp
public ScaledAnimationCurve drag = ScaledAnimationCurve.EaseInOut(0.01f, 0f, 2f, 1f, 3.5f);
```

This configures drag to increase from `2` to `3.5` over the `0–1` weight range, scaled down globally by `0.01`.
