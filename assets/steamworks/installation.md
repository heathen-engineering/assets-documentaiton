---
description: Installing Heathen Engineering's Steamworks and related componenets.
---

# Installation

## GitHub Sponsors

{% embed url="https://github.com/sponsors/heathen-engineering" %}

{% hint style="success" %}
Better for us and better for you!

Sponsoring Heathen on GitHub for $10 a month gets you access to the sorce repository for Steamworks, PhysKit and UX Complete.

\
See why GitHub sponsor is the hands down best way to Do More with Heathen in our [Licensing Article](../licensing/).
{% endhint %}

## New Installs

For new projects this couldn't be simplier.

Import into Unity as you normally would and it will install all dependencies for you.

## Updating Existing Installs

{% hint style="info" %}
When upgrading from Steamworks Foundation or Steamworks Complete versions 2.16.0 or earlier you should fully remove your existing install before importing the new Steamworks Foundation or Steamworks Complete package.



This will help insure a clean and efficient install process. This is due to System Core being moved out of Unity Asset Store and into GitHub as a dependency similar to Steamworks.NET. The asset will handle this install process for you but needs any old versions removed first.
{% endhint %}

{% hint style="warning" %}
**How to clean for re-install!**

If for any reason you want or need to clean your project for a fresh reinstall follow these simple steps



1\) Removal\
If you installed Steamworks Complete from Unity Asset Store, delete the \_Heathen Engineering folder

If you installed from Package Manager, remove it from Package Manager

2\) Remove Dependencies\
Remove Steamworks.NET ... if Steamworks Complete is the only Heathen asset you are using you can also remove System Core

3\) Remove Script Defines\
`HE_SYSCORE`, `HE_STEAMCOMPLET` and `STEAMWORKS_NET` can all be removed from your Player Settings > Script Defines



You are now ready to reinstall:

The **ONLY** thing you need to install your self is Steamworks Complete, it will handle the install of all other dependencies.
{% endhint %}

## Import

### GitHub Sponsors

If your a GitHub sponsor you have access to the source repository which you can install from directly in Unity via the Package Manager.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SourceRepo.git?path=/Steamworks/com.heathen.steamworkscomplete
```

GitHub will prompt you to login if you haven't already, this is how it checks to make sure your a sponsor and have access to the repo. Once done it will install Steamworks and any required dependencies.

### Free Foundation

Steamworks Foundaiton is a freely available "lite" version of Heathen's Steamworks system. It is available on GitHub as is, without warrenty. It is lisensed under the MIT license agreement with a Common Clause condition allowing you to use it for any purpose ... other than releasing a competating Steamworks Integraiton on the Unity Asset Store :sunglasses:

To install Steamworks Foundaiton&#x20;

This must be done from the Unity Package Manager to insure that the proper Steamworks Foundaiton assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SteamworksFoundation.git?path=/com.heathen.steamworksfoundation
```

### Unity Asset Store

If you purchased through the Unity Asset Store simply import through Unity's normal method.

Once imported the asset will check for dependencies and if missing it will install them via the Package Manager.

## Prerequisites

Heathen's Steamworks assets (both Foundaiton and Complete) will handle the install of all requirements for you. Our asset is also able to handle existing installs of its required componenets. You shouldn't need to do anything other than import our asset.

{% hint style="warning" %}
#### Legacy Code



If you have legacy, custom or otherwise not from the original source versions of Steamworks.NET or System Core then Unity will cause merge conflcits when importing our asset.



You should not be using versions of Steamworks.NET (or System Core) other than the version avialable from its author on GitHub such as would be installed by the Package Manger as discribed below and as installed by our asset on import into a clean project.



The single most common installation issue is due to having a full or partial install of an old or customized version of Steamworks.NET in your project when importing our asset. Our asset will not attempt to compile until Steamworks.NET is properly installed. It accomplishes this by only compiling when the script define `STEAMWORKS_NET` is defined.



If you have questions or issues pealse reach out on our [Discord ](https://discord.gg/6X3xrRc)channel
{% endhint %}

## Install Process

When you import Heathen's Steamworks (Foundation or Complete) it will test for the presence of Steamworks.NET and System Core and if missing it will ask you if you want to install those assets similar to the message shown below.

![](<../../.gitbook/assets/image (163) (1).png>)

When you click yes the system will use Package Manager to install Steamworks.NET and System Core from GitHub.&#x20;

{% hint style="info" %}
Installing Unity Packages via Git URL as we do here requires that you have Git installed. as outlined in [Unity's documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html).\
\
If you don't have it already you can install Git from the following link:

* [https://git-scm.com/](https://git-scm.com)&#x20;

Note that this does NOT mean you will be using Git as a source repo, it is simply a set of protocols used by Package Manager to download the required code from its target repository.
{% endhint %}

{% hint style="warning" %}
If you get a message to the effect of \
`No git executable was found`\
\
This video might help you get it resolved

[https://youtu.be/F-8A8mJwL\_Y](https://youtu.be/F-8A8mJwL\_Y)



We are not associated with the creator we have simply been told that video has helped others with that error.



This thread might also be of help for you

[https://forum.unity.com/threads/no-git-executable-was-found-please-install-git-on-your-system-and-restart-unity.730511/](https://forum.unity.com/threads/no-git-executable-was-found-please-install-git-on-your-system-and-restart-unity.730511/)
{% endhint %}

When Steamworks.NET is successfuly installed you will see messages in your console log similar to the following. These messages indicate what was installed, you can also review these in your Package Manager.

![](<../../.gitbook/assets/image (164) (1).png>)

{% hint style="info" %}
This always installs the latest code available and so the version number you see may very.
{% endhint %}

### I clicked no now what?

If for whatever reason you clicked no, or if you had an error and needed to install Git, or if you simply want to update Steamworks.NET or System Core you can always use the `Help > Heathen > Steamworks` menu entry to update any or all requriements.

&#x20;

![](<../../.gitbook/assets/image (179).png>)

## From Package Manager

If you dont like simply pressing buttons you can always install Steamworks.NET and System Core from the package manager your self.

### Install Steamworks.NET

This must be done from the Unity Package Manager to insure that the proper Steamworks.NET assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net
```

### Install System Core

This must be done from the Unity Package Manager to insure that the proper System Core assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SystemCore.git?path=/com.heathen.systemcore
```

### Install Heathen's Steamworks

#### For Steamworks Foundaiton

This must be done from the Unity Package Manager to insure that the proper Steamworks Foundaiton assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SteamworksFoundation.git?path=/com.heathen.steamworksfoundation
```

#### For Steamworks Complete

from the Package Manager

1. Open the Package Manager
2. Select the "My Assets" option&#x20;
3. Search for "Steamworks V2"\
   &#x20;![](<../../.gitbook/assets/image (148).png>)&#x20;
4. Click Import

## Manual Import

{% hint style="danger" %}
NOT RECOMENDED

This method is not recommended for the following reasons

1. The resulting import is directly in your project and its code can be changed inadvertently, often resulting in hard to track down errors
2. It requires manual steps that are easy to get wrong even when you have done them 100s of times
3. It makes it harder to keep your Steamworks.NET install up to date
{% endhint %}

{% hint style="danger" %}
**DO NOT USE THE RELEASE UNITYPACKAGE**

The .unitypackage available in Steamwork.NET's release folder is rarely up to date and often lacks important parts available from manual download and or the package manager, mainly the assembly definition file which our and many other assets are dependent on.
{% endhint %}

### Install Steamworks.NET

1. Navigate to Steamworks.NET's Git repo\
   [https://github.com/rlabrecque/Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET)
2. Select the "Code" button drop down in the upper right and select Download Zip\
   or\
   Simply click this link: [https://github.com/rlabrecque/Steamworks.NET/archive/refs/heads/master.zip](https://github.com/rlabrecque/Steamworks.NET/archive/refs/heads/master.zip)
3. Extract the code to your desktop or other folder location \
   Do **NOT** extract it to your Unity Project folder.
4. Open the folder and copy the sub folder "com.rlabrecque.steamworks.net"
5. Past the copied folder into your Unity project under your Assets folder such that you now have a folder in your project "./Assets/com.rlabrecque.steamworks.net"
6. Return to Unity and let it import the assets.

### Install Heathen's Steamworks

You can now install Heathen's Steamworks from Unity Package Manager

1. Open the Package Manager
2. Select the "My Assets" option&#x20;
3. Search for "Steamworks V2"\
   &#x20;![](<../../.gitbook/assets/image (148).png>)&#x20;
4. Click Import

## Uninstall

Removing any Heathen Engineering asset is as simple as deleting the folder. Heathen always installs under the `_Heathen Engineering` folder&#x20;

Each product will have an entry in the Assets, Documentation and Samples folders so for example

* \_Heathen Engineering
  * Assets
    * Steamworks
  * Documentation
    * Steamworks
  * Samples
    * Steamworks

If you only have 1 Heathen Engineering asset then you are safe to simply remove the whole \_Heathen Engineering folder.

Otherwise you can simply remove the folder corresponding to the product you want to remove.

## Technical Requirements

### Unity 2019 LTS or later

Heathen's Steamworks is dependent on features and frameworks of Unity's 2019 LTS. In particular the asset makes use of the UI Toolkit aka UI Elements framework to author custom inspector windows and tools.&#x20;

{% hint style="danger" %}
Older builds of Unity 2019 LTS had a known issue from Unity which would cause UI Toolkit to crash or otherwise fail. Unity corrected this issue in later 2019 LTS releases.

**You must update Unity 2019 LTS to the current latest build of Unity 2019 LTS before we can provide you with support on this issue.**
{% endhint %}

### Steamworks.NET

Heathen's Steamworks is built on top of Steamworks.NET and is dependent on it. You must install Steamworks.NET including its assembly definition in order for the Heathen Steamworks asset to work.

#### Steps

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net
```

When completed properly you will see Steamworks.NET in your Package Manager's "In Project" list. You can repeat the above steps to update Steamworks.NET at any time.

![](<../../.gitbook/assets/image (145).png>)

### Install System Core

This must be done from the Unity Package Manager to insure that the proper System Core assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SystemCore.git?path=/com.heathen.systemcore
```

![](<../../.gitbook/assets/image (166).png>)

## Networking Integrations

Heathen Engineering works with the communities of other assets and tools to help insure a smooth and efficient integration between our technologies. In particular Heathen has invested notable effort in the networking transports of the following solutions and works to insure they function properly with the Steamworks.NET APIs and with our own Steamworks tools.

### DarkRift2

{% embed url="https://assetstore.unity.com/packages/tools/network/darkrift-networking-2-pro-95399" %}

> DarkRift takes a code-first approach to cloud based networking to make a super simple and super easy to learn networking solution that can be used for absolutely any type of game.

#### Steam P2P Transport

{% hint style="danger" %}
This transport is written to work with Facepunch and doesn't make proper use of the SteamGameServer APIs and so is limited to P2P.\
\
If you want to use this transport you will need to port it to use Steamworks.NET which should be trivial.&#x20;

\
If you wanted to use it with Client/Server architectures then you would need to wrap its calls to use the proper API based on build i.e.

\
Code written like this&#x20;

```csharp
SteamNetworkingUtils.InitRelayNetworkAccess();
```

\
should be rewritten to look like this.

```csharp
#if UNITY_SERVER
                SteamGameServerNetworkingUtils.InitRelayNetworkAccess();
#else
                SteamNetworkingUtils.InitRelayNetworkAccess();
#endif
```
{% endhint %}

{% embed url="https://github.com/nico1207/DarkRift2_Steamworks_P2P_Sockets" %}

### FishNetworking

{% embed url="https://assetstore.unity.com/packages/tools/network/fish-net-networking-evolved-207815" %}

> A feature-rich Unity networking solution aimed towards reliability, ease of use, efficiency, and flexibility. Developed by a professional game designer, supported by the community.

The developer of FishNetworking has worked with Heathen Engineering developers to insure its Steam Transport is compatible with Steamworks V2 and with Steamworks.NET in general.

#### Requirements

You must install FishNetworking from Git Hub along with its Fishy Steam transport.

#### Installation

FishNetworking is available on git hub and includes documentation for installation there.

{% embed url="https://github.com/FirstGearGames/FishNet" %}

### Mirror

Mirror is a community lead project based on Unity's abandoned uNET. Mirror is (in Heathen's opinion) the most robust high level networking interface (HLAPI) currently available for Unity and is the main HLAPI used by Heathen Engineering.

Mirror has various transports including a Heathen compatible Steam Networking and Steam Sockets transport. Heathen Engineering does not author this transport but does contribute to its ongoing maintenance insuring proper use of the Steam APIs and compatibility with Heathen's Steamworks assets.

{% embed url="https://assetstore.unity.com/packages/tools/network/mirror-129321" %}

{% embed url="https://github.com/vis2k/Mirror" %}

#### Requirements

You must install the base of Mirror first, this can be done either from the Unity Asset Store via the Unity Package Manger or via GitHub.

#### Transports

{% embed url="https://github.com/Chykary/FizzySteamworks/" %}

Mirror Community's FizzySteamTransport has been made compatible with our asset and has been updated to support Peer to Peer and Client Server based networking architectures. The steps to install it are as follows.

**To install FizzySteamworks**

1. Open Unity 2019 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
5. Enter the URL below and press the add button:

```
https://github.com/Chykary/FizzySteamworks.git?path=/com.mirror.steamworks.net
```

### NetCode for GameObjects

NetCode (formerly MLAPI) was originally similar to Mirror in that it was an open source community lead project and had many similarities ot uNET. Unity Technology invested in NetCode and took over the project a few years ago and have been developing it as the new HLAPI from Unity.

{% embed url="https://docs-multiplayer.unity3d.com/" %}

#### Requirements

You must install Unity's NetCode to use its community transports. The above article is the best source to learn how to install and update NetCode. The notes provided here should work for you though are not keep up to date. Please consult Unity's official NetCode documentation for any questions or support needs.

**To install NetCode for GameObjects**

1. Open Unity 2020 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
5. Enter the URL below and press the add button:

```
com.unity.netcode.gameobjects
```

#### Transports

{% embed url="https://github.com/Unity-Technologies/multiplayer-community-contributions/tree/main/Transports/com.community.netcode.transport.steamnetworking" %}
Steam Networking Transport
{% endembed %}

NetCode for GameObjects has a community transport project similar to other HLAPI frameworks. Heathen Engineering has contributed a transport that is compatible with Steamworks.NET and can be downloaded from Unity's community transports section.

**To install the transport**

1. Open Unity 2020 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
5. Enter the URL below and press the add button:

```
https://github.com/Unity-Technologies/mlapi-community-contributions.git?path=/Transports/com.community.netcode.transport.steamnetworking
```
