# Float Stat

## Definition

```csharp
public class FloatStatObject : StatObject
```

Represents a float stat, consult the Steam Documentation for the specific use cases for each of the stat types

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

### Fields and Attributes

| Type  | Name  | Comment                      |
| ----- | ----- | ---------------------------- |
| float | Value | Get or set the current value |

### Methods

{% hint style="danger" %}
Other methods are available but should not be used and exist only for compatability with the generic StatObject interface.
{% endhint %}

Updates the stat

```csharp
public void StoreStas();
```

Calls Store Stats on the the Steam API
