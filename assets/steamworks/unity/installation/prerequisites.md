---
description: If you don't do this you will have problems
---

# Prerequisites

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Heathen's Steamworks assets (both Foundation and Complete) will handle the install of all requirements for you. Our asset is also able to handle existing installs of its required components. You shouldn't need to do anything other than import our asset.

{% hint style="warning" %}
#### Legacy Code



If you have legacy, custom or otherwise not from the original source versions of Steamworks.NET or System Core then Unity will cause merge conflicts when importing our asset.



You should not be using versions of Steamworks.NET (or System Core) other than the version available from its author on GitHub such as would be installed by the Package Manger as described below and as installed by our asset on import into a clean project.



The single most common installation issue is due to having a full or partial install of an old or customized version of Steamworks.NET in your project when importing our asset. Our asset will not attempt to compile until Steamworks.NET is properly installed. It accomplishes this by only compiling when the script define `STEAMWORKS_NET` is defined.



If you have questions or issues please reach out on our [Discord ](https://discord.gg/6X3xrRc)channel
{% endhint %}

## Unity 2020 LTS or later

Heathen's Steamworks is dependent on features and frameworks of Unity's 2020 LTS. In particular the asset makes use of the UI Toolkit aka UI Elements framework to author custom inspector windows and tools.&#x20;

## Unity Mathematics

{% hint style="info" %}
This will be installed for you by the installation process. It is a requirement for a number of assets so may already be present. This cannot be installed manually and is available from Unity's package repository.
{% endhint %}

{% embed url="https://docs.unity.cn/Packages/com.unity.mathematics@1.2/manual/index.html" %}

{% embed url="https://www.youtube.com/watch?v=u9DzbBHNwtc" %}

## System Core

{% hint style="info" %}
This will be installed for you by the installation process. It does use Unity's Package Manager's Add from Git URL and as such requires that you have Git installed properly.\
\
You can install System Core manually by simply copying its code into your project if you choose but this is not recommended.
{% endhint %}

{% embed url="https://github.com/heathen-engineering/SystemCore" %}

Heathen's [System Core](../../../system-core/) is an open source framework built around Unity's Scriptable Objects and is the bases for all of Heathen's own assets.

### Install from UPM

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SystemCore.git?path=/com.heathen.systemcore
```

## Steamworks.NET

{% hint style="info" %}
This will be installed for you by the installation process. It does use Unity's Package Manager's Add from Git URL and as such requires that you have Git installed properly.\
\
You can install Steamworks.NET manually by simply copying its code into your project if you choose but this is not recommended.
{% endhint %}

{% embed url="https://github.com/rlabrecque/Steamworks.NET" %}

[Steamworks.NET](https://steamworks.github.io/) is an open source C# wrapper around Valve's Steam API and is a true one to one wrap.

### Install from UPM

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net
```

###
