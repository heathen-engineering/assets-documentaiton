# Verlet Transform Tree

A simulation structure for animating hierarchical transforms using Verlet integration. Typically used for tails, ropes, chains, or foliage where child transforms follow dynamic, physics-based motion.

The `VerletTransformTree` defines and simulates a single transform hierarchy using Verlet physics. It handles node registration, per-frame simulation updates, and optional collision resolution based on settings curves. Each node retains a reference to its transform and original pose for positional and rotational constraints.

***

### Public Fields

### Root

```csharp
public Transform root;
```

The root transform of the simulated hierarchy. All children (excluding those in `ignoreList`) will be registered as nodes.

***

### Settings

```csharp
public VerletTransformTreeSettings settings;
```

Reference to a `VerletTransformTreeSettings` asset that defines spring, damping, angle limits, drag, and collision curves based on depth in the hierarchy.

***

### Ignore List

```csharp
public List<Transform> ignoreList = new List<Transform>();
```

Any transforms to exclude from simulation. Useful for skipping specific branches of the hierarchy or static bone references.

***

### Nodes

```csharp
public List<VerletTransformNode> nodes = new List<VerletTransformNode>();
```

The list of simulated nodes in the hierarchy. Each node stores initial transform data and current simulation state.

***

### Show Debug

```csharp
public bool showDebug = false;
```

If enabled, node data and wire representations (capsules, links) will be drawn in the Scene view.

***

### Public Methods

### Register Nodes

```csharp
[ContextMenu("Register Nodes")]
public void RegisterNodes()
```

Scans the transform hierarchy starting from `root` and populates the `nodes` list. Excludes any transforms in `ignoreList`.

***

### Add Force

```csharp
public void AddForce(Vector3 force)
```

Applies a global directional force to all nodes in the hierarchy.

***

### Add Force at Position

```csharp
public void AddForceAtPosition(float forceMagnitude, Vector3 position)
```

Applies a radial force from a given world position, diminishing by distance. Useful for explosions or impacts.

***

### Clear Forces

```csharp
public void ClearForces()
```

Clears accumulated external forces from all nodes.

***

### Reinitialise

```csharp
public void Reinitialise()
```

Resets all nodes to their original transform state and clears accumulated simulation data. Typically used after editing hierarchy structure in-editor.

***

## Example Usage

### Basic Setup

Attach a `VerletTransformTree` component to a GameObject and assign the root transform (e.g. a bone or empty parent).

Assign a `VerletTransformTreeSettings` asset to configure spring behaviour.

Optionally use the context menu "Register Nodes" to initialise the node hierarchy.

***

### Runtime Force Application

```csharp
public class TailWhip : MonoBehaviour
{
    public VerletTransformTree tree;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            tree.AddForce(Vector3.right * 5f);
        }
    }
}
```

This applies a one-time directional force to all nodes in the tree.
