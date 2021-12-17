---
description: Installing Heathen Engineering's Steamworks and related componenets.
---

# Installation

Once you have meet the requirements listed below the only step you need to perform is to import the package from Unity into your project.

## Package Manager Install

{% hint style="info" %}
Installing Unity Packages via Git URL as we do here requires that you have Git installed. as outlined in [Unity's documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html).\
\
If you don't have it already you can install Git from the following link:

* [https://git-scm.com/](https://git-scm.com) (classic but less user friendly)

Note that this does NOT mean you will be using Git as a source repo, it is simply a set of protocols used by Package Manager to download the required code from its target repository.
{% endhint %}

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

### Install Heathen's Steamworks&#x20;

from the Package Manager

1. Open the Package Manager
2. Select the "My Assets" option&#x20;
3. Search for "Steamworks V2"\
   &#x20;![](<../../.gitbook/assets/image (148).png>)&#x20;
4. Click Import

## Manual Install

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

You can now install Heathen's Stemworks from Unity Pacakge Manager

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

## Requirements

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

## Networking Integrations

Heathen Engineering works with the communities of other assets and tools to help insure a smooth and efficient integration between our technologies. In particular Heathen has invested notable effort in the networking transports of the following solutions and works to insure they function properly with the Steamworks.NET APIs and with our own Steamworks tools.

### FishNetworking (Beta)

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

NetCode for GameObjects has a community transport project similar to other HLAPI frameworks. Hethen Engineering has contributed a transport that is compatable with Steamworks.NET and can be downloaded from Unity's community transports section.

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
