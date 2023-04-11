---
description: When you need it on-demand
---

# Steamworks Creator

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

The Steamworks Creator exists to selectivly create a [Steamworks Behaviour](steamworks-behaviour.md) object for you based on the current state of Steam API initalziation. This componenet can be used in every scene and will test for Steam intialization and if required will create a new [Steamworks Behaviour](steamworks-behaviour.md) object as required, optionally marking it as Do Not Destroy on Load.

{% hint style="warning" %}
This component is an alternative for users that cannot or do not wish to use a bootstrap scene or otherwise insure that [Steamworks Behaviour](steamworks-behaviour.md) is initalized once and only once by design.



This tool performs a check on start and will if required create a new [Steamworks Behaivour](steamworks-behaviour.md) object. This is not as performant or as stable as adjusting your design such that there is one and only one [Steamworks Behaivour](steamworks-behaviour.md) object in your app but it does afford a degree of flexability.
{% endhint %}

### Use

Simply add a Steamworks Creator to a game object in any or even all scenes. The object can be configured to test on start or on demand and can be configured to mark the resulting [Steamworks Behaviour](steamworks-behaviour.md) object as Do Not Destroy.

![](<../../../../.gitbook/assets/image (151) (1) (1).png>)

### Create On Start

This configuration option if set true will cause the creator to check for Steam initalization at startup, if found it will do nothing if not it will create a new [Steamworks Behaivour](steamworks-behaviour.md) game object complete with the [Steamworks Behaviour](steamworks-behaviour.md) componenet and will apply the indicated Steam Settings object.

If this is not set to true you would need to call the Create If Missing method to perform the check and create on demand.

```csharp
steamworksCreator.CreateIfMissing();
```

{% hint style="info" %}
If you wish to create on-demand you can do so without the aid of the Steamworks Creator. SteamSettings has a static CreateBehaviour method that can be called to perform the same action.



```csharp
SteamSettings.CreatBehaviour(settings, markAsDoNotDestroy);
```
{% endhint %}

### Mark As Do Not Destroy

This configuration option if set true will cause the creator to mark the resulting GameObject as DoNotDestroyOnLoad. This is only applicable if the creator creates a new [Steamworks Beahviour](steamworks-behaviour.md) and is not used otherwise.

If not set then the created GameObject will reside in the currently active scene and will be destroyed when that scene is unloaded.&#x20;

{% hint style="danger" %}
You must not allow a [Steamworks Behaviour](steamworks-behaviour.md) object to be destroyed. Doing so will cause unperdictable errors with your Steam Integration.



If you do not mark as do not destroy then you must insure that the resulting GameObject is never destroyed.
{% endhint %}

### Settings

This is the settings object that will be applied to the resulting [Steamworks Behaivour](steamworks-behaviour.md), this MUST be set.
