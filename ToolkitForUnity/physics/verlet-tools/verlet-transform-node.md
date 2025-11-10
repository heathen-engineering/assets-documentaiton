# Verlet Transform Node

`VerletTransformNode` and `VerletTransformNode2D` are lightweight data containers used internally by the Verlet Physics Transform system to track the simulation state of individual `Transform` objects in 3D and 2D space, respectively.

Each node represents a point in a physics chain and stores the simulation state necessary for accurate Verlet integration, such as current and previous position, accumulated forces, and rest lengths between nodes. These nodes form the basis of physics-based hierarchies (trees) that respond to forces and simulate soft-body or chain-like behaviours.

***

## Classes

#### `VerletTransformNode` (3D)

Used for full 3D simulation with `float3` values.

#### `VerletTransformNode2D` (2D)

Used for constrained 2D simulation with `float2` values.

***

## Shared Fields

### Target

```csharp
public Transform target
```

The Unity `Transform` this node represents in the simulation.

***

### Parent

```csharp
public VerletTransformNode parent
```

The parent node in the simulation chain. Defines the rest position direction and helps determine constraints.

_2D variant:_

```csharp
public VerletTransformNode2D parent
```

***

### Distance

```csharp
public float distance
```

The rest distance between this node and its parent, used to maintain structural constraints.

***

### Add Force

```csharp
public float3 addedForce
```

_2D variant:_ `float2 addedForce`

Temporary force accumulator for external influences applied to this node during simulation.

***

### Weight

```csharp
public float weight
```

The relative weight of this node used to determine how strongly it resists motion.

***

### Position

```csharp
public float3 position
```

_2D variant:_ `float2 position`

The current simulated position of the node.

***

### Prev Position

```csharp
public float3 prevPosition
```

_2D variant:_ `float2 prevPosition`

The simulated position from the previous time step, required for Verlet integration.

***

### Prev Timestep

```csharp
public float prevTimestep
```

Time step used in the previous simulation tick. Used for stable time-step compensation.

***

### Init Local Position

```csharp
public float3 initLocalPosition
```

_2D variant:_ `float2 initLocalPosition`

The initial local position of the transform relative to its parent.

***

### Init Local Rotation

```csharp
public quaternion initLocalRotation
```

Initial local rotation stored for re-alignment or restoration.

***

### Length

```csharp
public float length
```

Optional override length for this node's connection to its parent. Used in bone-like chains to enforce fixed segment length.

***

## Notes

* These classes are not meant to be manipulated directly in user code.
* They are constructed and updated by the `VerletTransformTree` system to drive transform motion.
* Marked `[Serializable]` for use with Unity serialisation and editor debugging.
* Fields are `[HideInInspector]` where they are not intended for manual editing in the inspector, ensuring a cleaner interface.
