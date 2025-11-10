# Verlet Transform Tree Settings

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

A ScriptableObject asset defining physics parameters and limiter curves for a `VerletTransformTree`. Used to configure per-depth simulation behaviour such as drag, damping, and collision influence.

The `VerletTransformTreeSettings` asset allows designers to fine-tune the physics behaviour of a transform hierarchy using a set of scaled curves. These curves are sampled per node based on relative depth, enabling smooth transitions from root to tip in drag, elasticity, angle limits, and collision responses.

***

## Public Fields

### Constant Acceleration

```csharp
public float3 constantAcceleration = new Vector3(0, -9.81f, 0);
```

A constant force applied to all nodes each simulation step. Typically represents gravity.

***

### Drag

```csharp
public ScaledAnimationCurve drag;
```

Controls how much velocity is reduced per step. A higher drag value causes the node to lose energy more quickly.

***

### Damping

```csharp
public ScaledAnimationCurve damping;
```

Applies smoothing to motion between nodes, helping prevent jitter and overshooting.

***

### Elasticity

```csharp
public ScaledAnimationCurve elasticity;
```

Defines how much a node tries to return to its rest position. Higher values increase spring-like behaviour.

***

### Stiffness

```csharp
public ScaledAnimationCurve stiffness;
```

Controls how rigidly nodes maintain their length from parent nodes. High stiffness enforces fixed bone lengths.

***

### Collision Layers

```csharp
public LayerMask collisionLayers = 0;
```

Defines which layers are checked during node collision tests. Used when collision response is enabled via the `collision` curve.

***

### Collision

```csharp
public ScaledAnimationCurve collision;
```

Controls how strongly each node responds to collisions. Typically increases toward tips of chains or leaves.

***

### Angle

```csharp
public ScaledAnimationCurve angle;
```

Limits the angle between a node’s forward vector and its rest orientation. Useful for constraining extreme bending.

***

## Example Usage

### Creating a Settings Asset

1. Right-click in the Project window
2. Select **Create → Variables → Verlet Transform Tree Settings**
3. Assign the asset to a `VerletTransformTree` component

***

### Curve Tuning Example

* Set `drag` to increase with depth to dampen motion further from the root
* Set `collision` to 0 at the root and 1 at the tips to enable impact response only on free ends
* Set `angle` curve to gently enforce pose limits on mid-chain nodes
