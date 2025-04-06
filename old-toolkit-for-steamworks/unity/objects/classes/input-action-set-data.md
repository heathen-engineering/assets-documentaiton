---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Input Action Set Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public struct InputActionSetData : IEquatable<InputActionSetHandle_t>, 
                                   IComparable<InputActionSetHandle_t>, 
                                   IEquatable<ulong>, 
                                   IComparable<ulong>
```

A wrapper around the InputActionSetHandle\_t structure from Valve's Steam API. This struct provides a lot of quality of life improvements over the native handle type and can be used interchangeably with it.

## Fields and Attributes

### Handle

The raw ulong value of the handle

```csharp
public ulong Handle { get; set; }
```

## Methods

### IsActive

```csharp
public bool IsActive(InputControllerData controller)
```

or

```csharp
public bool IsActive(InputHandle_t controller)
```

Checks if this set is active for the indicated controller

### Activate

```csharp
public void Activate(InputControllerData controller)
```

or

```csharp
public void Activate(InputHandle_t controller)
```

Activates this set on the indicated controller

### Get

```csharp
public static InputActionSetData Get(string setName)
```

or

```csharp
public static InputActionSetData Get(InputActionSetHandle_t handle)
```

or

```csharp
public static InputActionSetData Get(ulong handleValue)
```

This will get (i.e. find) the InputActionSetData based on the provided input e.g. its name or handle value.
