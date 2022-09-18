# Input Action Update

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Used by [InputAction ](input-action.md)objects to report changes as an event argument. InputAction is a type of Game Event, to learn more about [Game Events read our article here](../../system-core/game-events.md).

## Fields and Attributes

### controller

```csharp
public InputHandle_t controller
```

The controller this event was triggered by

### type

```csharp
public InputActionType type
```

The type of input action that caused this event

### mode

```csharp
public EInputSourceMode mode
```

The input mode behaviour used for the InputAction that generated this event e.g. button, stick, trigger, etc.

### isActive

```csharp
public bool isActive
```

Indicates rather or not this action is currently active

### isState

```csharp
public bool isState
```

Indicates rather or not this action is currently state == true or false, true meaning this action happened, false meaning it is not happening.

### isX

```csharp
public float isX
```

The current value of the X input for this action if any

### isY

```csharp
public float isY
```

The current value of the Y input for this action if any

### wasActive

```csharp
public bool wasActive
```

Indicates rather or not this action was active before this event

### wasState

```csharp
public bool wasState
```

Indicates rather or not this action was state = true or false before this event

### wasX

```csharp
public float wasX
```

The value of the X input for this action before this event if any

### wasY

```csharp
public float wasY
```

The value of the Y input for this action before this event if any

### DeltaX

```csharp
public float DeltaX => isX - wasX;
```

The difference between is and was for the X input

### DeltaY

```csharp
public float DeltaY => isY - wasY;
```

The difference between is and was for the Y input

### Active

```csharp
public bool Active => isActive;
```

Reads the is Active, convenance feature and no different than reading isActive

### State

```csharp
public bool State => isState;
```

Reads the is State, convenance feature and no different than reading isState

### X

```csharp
public float X => isX;
```

Reads the is X, convenance feature and no different than reading isX

### Y

```csharp
public float Y => isY;
```

Reads the is Y, convenance feature and no different than reading isY

### Data

```csharp
public InputActionData Data => get;
```

Returns an [InputActionData ](input-action-data.md)object representing the "is" or current state of the [InputAction](input-action.md).
