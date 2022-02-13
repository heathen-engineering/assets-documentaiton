# Float Stat

## Definition

```csharp
public class FloatStatObject : StatObject
```

Represents a float stat, consult the Steam Documentation for the specific use cases for each of the stat types

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Fields and Attributes

### Value

```csharp
public float Value { get; set; }
```

Reads or writes the value of this stat.

## Methods

{% hint style="danger" %}
Other methods are available but should not be used and exist only for compatability with the generic StatObject interface.
{% endhint %}

### Store Stats

```csharp
public void StoreStats();
```

Calls Store Stats on the the Steam API
