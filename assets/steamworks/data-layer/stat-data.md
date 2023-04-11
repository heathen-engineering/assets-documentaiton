# Stat Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public struct StatData : IEquatable<StatData>, 
                         IEquatable<string>, 
                         IComparable<StatData>, 
                         IComparable<string>
```

A data wrapper around Steam's concept of a stat. This is implicitly convertible from string expecting that string to be the "API Name" of the stat.

```csharp
StatData myStat = "NumGames";
myStat.Set(42);
myStat.Store();

Debug.Log($"NumGames = {myStat.IntValue()}");
```

## Fields and Attributes

### Id

```csharp
public string id;
```

The API name of the achievement.

## Methods

### FloatValue

```csharp
public float FloatValue()
```

Returns the float value of the stat.

### IntValue

```csharp
public int IntValue()
```

Returns the int value of the stat.

### RequestUserStats

```csharp
public void RequestUserStats(UserData user, 
                             Action<UserStatsReceived_t, bool> callback)
```

Requests the stats of a specific user be downloaded from Valve's servers. The callback on this inidicates when the request is completed along with its status ... the handler would look similar to the following

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

### GetValue

For use after you have called RequestUserStats, this gets the value for a specific user and has two overloads one for int values and one for float values.

```csharp
public bool GetValue(UserData user, out int value)
```

or

```csharp
public bool GetValue(UserData user, out float value)
```

If the method returns false the stat was not found, if it returns true then the value will be populated with the result.

### Set

```csharp
public void Set(float value)
```

Sets the float value of the stat.

```csharp
public void Set(int value)
```

Sets the int value of the stat.

```csharp
public void Set(float value, double length)
```

Updates the average rate state value of the stat.

### Store

```csharp
public void Store()
```

A simple short cut to the Stats and Achievements Store Stats and achievements. You can call this on any achievement or stat and it will commit all changes to the backend for all stats and achievements.
