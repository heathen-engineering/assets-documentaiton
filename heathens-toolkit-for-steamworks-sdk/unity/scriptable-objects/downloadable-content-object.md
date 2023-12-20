---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Downloadable Content Object

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The Downloadable Content Object is a scriptable object created by the Steam Settings when you import DLC. This can be used to check if the local user owns a given DLC and to perfrom common actions against that DLC.

{% hint style="info" %}
Most modern games do not actually download content with DLC rather they are usually only used as license to check if given content in the game should be unlocked.



This is in particular important for multiplayer games where you need all players to have all content in order to play together but want to lock/unlock content based on ownership of DLC aka expansions or modules.



It is however possible to assoceate a depot with DLC and have it actually download additional game content.
{% endhint %}

## Definition

```csharp
public class DownloadableContentObject : ScriptableObject
```

Represents a DLC object, this is created by the [Steam Settings](steam-settings/) object when you import DLC data for your app. To learn more see the [Steam Settings](steam-settings/) object documentation.

## Fields and Attributes

<table><thead><tr><th width="187.56643368118847">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>AppId_t</td><td>appId</td><td>The room this message relates to</td></tr><tr><td>bool</td><td>IsSubscribed</td><td>Indicates rather or not the DLC is currently owned</td></tr><tr><td>bool</td><td>IsInstalled</td><td>Indicated rather or not the DLC is installed</td></tr></tbody></table>

## Methods

### Get Install Directory

```csharp
public string GetInstallDirectory();
```

Returns the intall location of the DLC

### Get Download Progress

```csharp
public float GetDownloadProgress();
```

Returns the download progress if known as a value between 0 and 1

### Get Earliest Purchase Time

```csharp
public DateTime GetEarliestPurchaseTime();
```

Gets the time of purchase if known

### Install content

```csharp
public void Install();
```

Starts the process of installing the DLC

### Uninstall content

```csharp
public void Uninstall();
```

Starts the process of uninstalling the DLC

### Open Store

```csharp
public void OpenStore(flag);
```

Opens the Steam Overlay to the Store for this DLC item
