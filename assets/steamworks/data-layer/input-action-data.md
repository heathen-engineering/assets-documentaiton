# Input Action Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public struct InputActionData
```

Represents the current state of an input action and is returned by the InputAction and InputControllerData objects. Its not typical that you would create this your self. The most common use case is to use the GetActionData() method of the InputAction object in Unity or to use the API.Input class to get the action data of a specific controller.

## Fields and Attributes

### Name

The name of the action the data relates to

```csharp
public string name;
```

### Type

The type of action the data relates to

```csharp
public InputActionType type;
```

### Controller

The handle for the controller this action data relates to

```csharp
public InputHandle_t controller;
```

### Active

Is the action active or not

```csharp
public bool active;
```

### Mode

The type of input source this action reported

```csharp
public EInputSourceMode mode;
```

### State

The current state of the action at the time this data was generated

```csharp
public bool state;
```

### X

The x axis value of this input

```csharp
public float x;
```

### Y

The y axis value of this input

```csharp
public float y;
```
