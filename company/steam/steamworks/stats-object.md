---
description: Understanding Steam Stats and the Heathen Engineering tool kit
---

# Stats

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../">Guides and Tutorials</a></td><td><a href="../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../assets/physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../assets/ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% hint style="warning" %}
Please note that you must call StoreStatsAndAchievements to apply changes to the Steam backend, and thus cause the notification to pop up.

```csharp
API.StatsAndAchievements.Client.StoreStats();
```
{% endhint %}

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Creating Stats

Stats work much like achievements however they cannot be imported from Valve directly so you must add your stats to your system manually.

![](<../../../.gitbook/assets/image (188) (1) (1) (1).png>)

Once you add a sate you need to provide its API name exactly as you created it in the Steam Developer Portal.

![](<../../../.gitbook/assets/image (160) (1) (1).png>)

## Using Stats

See the [Int Stat Object](../../../assets/steamworks/unity/scriptable-objects/int-stat.md), [Float Stat Object](../../../assets/steamworks/unity/scriptable-objects/float-stat.md) and [Avg Rate Stat Object](../../../assets/steamworks/unity/scriptable-objects/avg-rate-stat.md) for details on how to use each. In general though the process is that you will create a reference to the stat in question in one of your game's scripts such as

```csharp
public IntStatObject myIntStat;
```

This will make a new reference slot you can drag and drop your stat into on the Unity inspector for that object.

![](<../../../.gitbook/assets/image (174) (1) (1) (1).png>)

You can now drag the desired stat object from your Steam Setting into that slot.

![](<../../../.gitbook/assets/image (159) (1) (1) (1).png>)

![](<../../../.gitbook/assets/image (161) (1) (1) (1) (1) (1).png>)

Your script can now perform actions in relation to that stat

```csharp
// Read the stat value
Debug.Log("Value is " + myIntStat.Value);

// Set the stat value
myIntStat.Value = 42;

// Store the stat values (effects all stats)
myIntStat.StorStats();
```

