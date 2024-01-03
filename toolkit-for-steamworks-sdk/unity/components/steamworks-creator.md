---
description: When you need it on-demand
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Steamworks Creator

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Steamworks Creator exists to selectivly create a [Steamworks Behaviour](steamworks-behaviour.md) object for you based on the current state of Steam API initalziation. This componenet can be used in every scene and will test for Steam intialization and if required will create a new [Steamworks Behaviour](steamworks-behaviour.md) object as required, optionally marking it as Do Not Destroy on Load.

{% hint style="warning" %}
This component is an alternative for users that cannot or do not wish to use a bootstrap scene or otherwise insure that [Steamworks Behaviour](steamworks-behaviour.md) is initalized once and only once by design.



This tool performs a check on start and will if required create a new [Steamworks Behaivour](steamworks-behaviour.md) object. This is not as performant or as stable as adjusting your design such that there is one and only one [Steamworks Behaivour](steamworks-behaviour.md) object in your app but it does afford a degree of flexability.
{% endhint %}

### Use

Simply add a Steamworks Creator to a game object in any or even all scenes. The object can be configured to test on start or on demand and can be configured to mark the resulting [Steamworks Behaviour](steamworks-behaviour.md) object as Do Not Destroy.

![](<../../../.gitbook/assets/image (272).png>)

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
