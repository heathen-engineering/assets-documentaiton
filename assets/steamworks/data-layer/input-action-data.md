# Input Action Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

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
