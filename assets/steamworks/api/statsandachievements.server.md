# StatsAndAchievements.Server

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

```csharp
using StatsServer = HeathenEngineering.SteamworksIntegration.API.StatsAndAchievements.Server;
```

```csharp
public static class StatsAndAchievements.Server
```

All features available to 1 are present in the other with some minor exceptions. The only notable difference is that Server related calls required you to provide the CSteamID of the user to be adjusted and will only work when that user is authenticated to the Steam Game Server that calls the method.

### What can it do?

Set and reset Steam Stats and Achievements. Most of the features of the StatsAndAchievments interface can be accessed through its related objects.

### Related Obejcts

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/avg-rate-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/float-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/int-stat" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/achievement-object" %}
