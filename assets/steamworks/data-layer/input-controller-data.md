# Input Controller Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

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
