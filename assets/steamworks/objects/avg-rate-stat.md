# Avg Rate Stat

## Definition

```csharp
public class AvgRateStatObject : StatObject
```

Represents a AvgRat stat, consult the Steam Documentation for the specific use cases for each of the stat types

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Fields and Attributes

| Type  | Name  | Comment                       |
| ----- | ----- | ----------------------------- |
| float | Value | The current value of the stat |

## Methods

{% hint style="danger" %}
Other methods are available but should not be used and exist only for compatability with the generic StatObject interface.
{% endhint %}

### Update Stat

```csharp
public void UpdateAvgRateStat(value, length);
```

Updates the stat

### Store Stats

```csharp
public void StoreStas();
```

Calls Store Stats on the the Steam API
