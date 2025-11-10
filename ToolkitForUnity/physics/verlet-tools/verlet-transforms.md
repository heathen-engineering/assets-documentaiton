# Verlet Transforms

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

A MonoBehaviour component for simulating soft-body or chain-like animation behaviour using Verlet integration applied to multiple `VerletTransformTree` instances. Typically used to drive physics-like behaviours on bones, joints, or pseudo-rigid chains.

The `VerletTransforms` component acts as a controller that manages one or more `VerletTransformTree` objects. Each tree defines a hierarchy of nodes that simulate physics-based motion via Verlet integration. This component provides global controls for registering nodes and applying forces, and it draws gizmos for visual debugging in the editor.

## Public Fields

### Show Gizmo

```csharp
public bool showGizmo = true;
```

If enabled, gizmos will be drawn in the Scene view to visualise the simulated hierarchies.

### Transfrom Hierarchies

```csharp
public List<VerletTransformTree> transformHierarchies = new List<VerletTransformTree>();
```

The list of managed transform trees. Each `VerletTransformTree` handles its own node hierarchy and settings.

### Public Methods

### Register Trees

```csharp
csharpCopyEdit[ContextMenu("Register Nodes")]
public void RegisterTrees()
```

Registers all nodes in the `transformHierarchies`. This is typically called once at startup, but can be called manually to refresh the node layout in-editor.

***

### Add Force

```csharp
public void AddForce(Vector3 force)
```

Applies a global directional force to all transform trees.

***

### Add Force At Position

```csharp
public void AddForceAtPosition(float forceMagnitude, Vector3 position)
```

Applies a radial force from a specific world position to all transform trees.

***

### Add Force

```csharp
public void AddForce(int treeIndex, Vector3 force)
```

Applies a force to a specific tree by index. If the index is invalid, a warning is logged.

***

### Get Tree

```csharp
public VerletTransformTree GetTree(int index)
```

Returns a tree from `transformHierarchies` at the given index. Logs a warning if the index is invalid.

***

## Example Usage

#### Basic Setup

1. Add `VerletTransforms` to a GameObject.
2. Assign one or more `VerletTransformTree` instances in the inspector.
3. Optionally, use the context menu **"Register Nodes"** to initialise the tree.

### Applying Forces at Runtime

Generally input happens by moving the object or other objects moving into it (collision) however you can also inject force such as from an explosion or wind.

```csharp
public class ShakeAllTrees : MonoBehaviour
{
    public VerletTransforms verlet;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.F))
        {
            verlet.AddForce(Vector3.up * 10f);
        }
    }
}
```
