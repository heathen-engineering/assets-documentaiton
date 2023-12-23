---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Int Stat

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class IntStatObject : StatObject
```

Represents an int stat, consult the Steam Documentation for the specific use cases for each of the stat types

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Fields and Attributes

### Value

```csharp
public int Value { get; set; }
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

### Request User Stats

```csharp
public void RequestUserStats(UserData user, 
                             Action<UserStatsReceived_t, bool> callback)
```

Requests the stats of a specific user be downloaded from Valve's servers. The callback on this indicates when the request is completed along with its status ... the handler would look similar to the following

```csharp
void HandleCallback(UserStatsRecieved_t results, bool IOError)
{
    if(!IOError 
        && results.m_eResult == EResult.k_EResultOK)
    {
        //We now have the stats for this user
    }
}
```

### Get Value

For use after you have called RequestUserStats, this gets the value for a specific user and has two overloads one for int values and one for float values.

```csharp
public bool GetValue(UserData user, out int value)
```

or

```csharp
public bool GetValue(UserData user, out float value)
```

If the method returns false the stat was not found, if it returns true then the value will be populated with the result.
