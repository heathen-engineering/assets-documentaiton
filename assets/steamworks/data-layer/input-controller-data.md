# Input Controller Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public struct InputControllerData
```

Returned as a result of the [API.Input.Client.Update(...)](../api/input.md#update) method this contains all the current action data and report of changes since the last update was ran for a specific controller.

## Fields and Attributes

### Handle

The controller handle this data is for

```csharp
public InputHandle_t handle;
```

### Inputs

A collection of InputActionData for every tracked Input Action available

```csharp
public InputActionData[] inputs;
```

### Changes

A collection of InputActionUpdate for each input action whose current state differs from its previous e.g. what changed this frame.

```csharp
public InputActionUpdate[] changes;
```

## Methods

### Get Action Data

Returns the InputActionData for a specified action

```csharp
public InputActionData GetActionData(InputAction action)
```

or

```csharp
public InputActionData GetActionData(string name)
```

### Get Active

Returns the "active" value for a specified action

```csharp
public bool GetActive(string name)
```

### Get State

Returns the "state" value for a specified action

```csharp
public bool GetState(string name)
```

### Get Float

Returns the "float" value for a specified action

```csharp
public float GetFloat(string name)
```

### Get Float2

Returns the "float2" value for a specified action

```csharp
public float2 GetFloat2(string name)
```
