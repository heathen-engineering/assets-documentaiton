---
description: Installing Heathen Engineering's Steamworks and related componenets.
---

# Installation

Once you have meet the requirements listed below the only step you need to perfrom is to import the package from Unity into your project.

## Package Manager Install

{% hint style="info" %}
Installing Unity Packages via Git URL as we do here requires that you have Git installed. as outlined in [Unity's documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html).\
\
If you dont have it already you can install Git from the following link:

* [https://git-scm.com/](https://git-scm.com) (classic but less user friendly)

Note that this does NOT mean you will be using Git as a source repo, it is simply a set of protocols used by Package Manager to download the required code from its target repository.
{% endhint %}

1. Install Steamworks.NET \
   This must be done from the Unity Package Manager to insure that the proper Steamworks.NET assembly definition is installed and present in your project.
   1. Open the Package Manager
   2. Click the "+" (plus) button located in the upper left of the window
   3. Select the "Add package from git URL..." option\
      ![](<../../.gitbook/assets/image (144).png>)
   4. Enter the following URL:\
      [https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net](https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net)
   5. Click the "Add" button and wait several seconds for the system to download and install the Steamworks.NET package from GitHub.
2. Install Heathen's Steamworks from the Package Manager
   1. Open the Package Manager
   2. Select the "My Assets" option&#x20;
   3. Search for "Steamworks V2"\
      &#x20;![](<../../.gitbook/assets/image (148).png>)&#x20;
   4. Click Import

## Manual Install

{% hint style="danger" %}
NOT RECOMENDED

This method is not recomended for the following reasons

1. The resulting import is directly in your project and its code can be changed inadvertently ... offten resulting in hard to track down errors
2. It requires manual steps that are easy to get wrong even when you have done them 100s of times
3. It makes it harder to keep your Steamworks.NET install up to date
{% endhint %}

{% hint style="danger" %}
**DO NOT USE THE RELEASE UNITYPACKAGE**

The .unitypackage available in Steamwork.NET's release folder is rarely up to date and offten lacks important parts available from manual download and or the package manager, mainly the assembly defintion file which our and many other assets are dependent on.
{% endhint %}

1. Install Steamworks.NET
   1. Navigate to Steamworks.NET's Git repo\
      [https://github.com/rlabrecque/Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET)
   2. Select the "Code" button drop down in the upeer right and select Download Zip\
      or\
      Simply click this link: [https://github.com/rlabrecque/Steamworks.NET/archive/refs/heads/master.zip](https://github.com/rlabrecque/Steamworks.NET/archive/refs/heads/master.zip)
   3. Extract the code to your desktop or other folder location \
      Do **NOT** extract it to your Unity Project folder.
   4. Open the folder and copy the sub folder "com.rlabrecque.steamworks.net"
   5. Past the copied folder into your Unity project under your Assets folder such that you now have a folder in your project "./Assets/com.rlabrecque.steamworks.net"
   6. Return to Unity and let it import the assets.
2. You can now install Heathen's Stemworks from Unity Pacakge Manager
   1. Open the Package Manager
   2. Select the "My Assets" option&#x20;
   3. Search for "Steamworks V2"\
      &#x20;![](<../../.gitbook/assets/image (148).png>)&#x20;
   4. Click Import

## Requirements

### Unity 2019 LTS or later

Heathen's Steamworks is dependent on features and frameworks of Unity's 2019 LTS. In particular the asset makes use of the UI Toolkit aka UI Elements framework to author custom inspector windows and tools.&#x20;

{% hint style="danger" %}
Older builds of Unity 2019 LTS had a known issue from Unity which would cause UI Toolkit to crash or otherwise fail. Unity corrected this issue in later 2019 LTS releases.

**You must update Unity 2019 LTS to the current latest build of Unity 2019 LTS before we can provide you with support on this issue.**
{% endhint %}

### Steamworks.NET

Heathen's Steamworks is built ontop of Steamworks.NET and is dependent on it. You must install Steamworks.NET including its assembly defintion in order for the Heathen Steamworks asset to work.

#### Steps

1. Open Unity 2019 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
5. Enter the following URL:\
   [https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net](https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net)
6. Click the "Add" button and wait several seconds for the system to download and install the Steamworks.NET package from GitHub.

When completed properly you will see Steamworks.NET in your Package Manager's "In Project" list. You can repeate the above steps to update Steamworks.NET at any time.

![](<../../.gitbook/assets/image (145).png>)

## Networking Integrations

Heathen Engineering works with the communities of other assets and tools to help insure a smooth and efficent integration between our technologies. In particular Heathen has invested notable effort in the networking transports of the following solutions and works to insure they funciton properly with the Steamworks.NET APIs and with our own Steamworks tools.

### FishNetworking (Beta)

> A feature-rich Unity networking solution aimed towards reliability, ease of use, efficiency, and flexibility.Developed by a professional game designer, supported by the community.

The developer of FishNetworking has worked with Heathen Engineering developers to insure its Steam Transport is compatable with Steamworks V2 and with Steamworks.NET in general.

#### Requirements

You must install FishNetworking from Git Hub along with its Fishy Steam transport.

#### Installation

FishNetworking is available on git hub and includes documentation for installation there.

{% embed url="https://github.com/FirstGearGames/FishNet" %}

### Mirror

Mirror is a community lead project based on Unity's abandoned uNET. Mirror is (in Heathen's openion) the most robust high level networking interface (HLAPI) currently available for Unity and is the main HLAPI used by Heathen Engineering.

Mirror has various transports including a Heathen compatable Steam Networking and Steam Sockets transport. Heathen Engineering does not author this transport but does contirbute to its ongoing maintenance insuring proper use of the Steam APIs and compatability with Heathen's Steamworks assets.

{% embed url="https://assetstore.unity.com/packages/tools/network/mirror-129321" %}

{% embed url="https://github.com/vis2k/Mirror" %}

#### Requirements

You must install the base of Mirror first, this can be done either from the Unity Asset Store via the Unity Package Manger or via GitHub.

#### Transports

{% embed url="https://github.com/Chykary/FizzySteamworks/" %}

Mirror Community's FizzySteamTransport has been made compatable with our asset and has been updated to support Peer to Peer and Client Server based networking architectures. The steps to install it are as follows.

1. Download the FizzySteamTransport from GitHub, you want to download the source code not the release package.\
   [https://github.com/Chykary/FizzySteamworks/archive/refs/heads/master.zip](https://github.com/Chykary/FizzySteamworks/archive/refs/heads/master.zip)
2. Extract the provided code into your Unity Project

### MLAPI

MLAPI was originally similar to Mirror in that it was an open source community lead project and had many similarities ot uNET. Unity Technology invested in MLAPI and took over the project a few years ago and have been developing it as the new HLAPI from Unity.&#x20;

MLAPI is far more experiamental and lacks the maturity of other options it does however have more support from Unity its self. Heathen does not use MLAPI in its own projects so canonly provide limited support. We do however contribute to the on going development and maintenance of its community transports including the SteamTransport.

{% embed url="https://docs-multiplayer.unity3d.com/" %}

#### Requirements

You must install Unity's MLAPI to use its community transports. The above article is the best source to learn how to install and update MLAPI. The notes provided here should work for you though are not keep up to date. Please consult Unity's offical MLAPI documentaiton for any questions or support needs.

**To install MLAPI**

1. Open Unity 2019 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
5. Enter the following URL:\
   [https://github.com/Unity-Technologies/com.unity.multiplayer.mlapi.git?path=/com.unity.multiplayer.mlapi](https://github.com/Unity-Technologies/com.unity.multiplayer.mlapi.git?path=/com.unity.multiplayer.mlapi#release/0.1.0)
6. Click the "Add" button and wait several seconds for the system to download and install the package from GitHub.

#### Transports

{% embed url="https://github.com/JamesMcGhee/multiplayer-community-contributions/tree/main/Transports/com.mlapi.contrib.transport.steamnetworking" %}

MLAPI has a community transport project similar to other HLAPI frameworks. Hethen Engineering has contributed a variation of MLAPI's SteamP2P transport that correct multiple issues with the original transport.

Heathen's SteamNetworking transport for MLAPI is based on the existing SteamP2P transport and updates it to

* Remove dependency on a specifc build of Steamworks.NET
* Remove use of SteamManager making it compatable with any Steamworks.NET implamentation \
  Including Heathen's own Steamworks tools.
* Added support for Client Server architectures by leveraging the Steam Game Server Networking APIs in server builds
* Improved support for Peer to Peer architectures by correcting use of the Steam Client Networking APIs

**To install the transport**

1. Open Unity 2019 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   ![](<../../.gitbook/assets/image (144).png>)
5. Enter the following URL:\
   [https://github.com/Unity-Technologies/mlapi-community-contributions.git?path=/Transports/com.mlapi.contrib.transport.steamnetworking](https://github.com/Unity-Technologies/mlapi-community-contributions.git?path=/Transports/com.mlapi.contrib.transport.steamnetworking)\
   Click the "Add" button and wait several seconds for the system to download and install the package from GitHub.

### Mirage Net (Informational)

{% hint style="warning" %}
This entry is here for informational purposes only

Heathen does not directly support Mirage and has not engaged with its community transport project as of yet.
{% endhint %}

From the same team that brought you Mirror, Mirage Net is a new open source networking framework. The project is not considered as mature as Mirror though it may be of interest to you. As the HLAPI is based on Mirror it should be trivial to port the Mirror based transport to Mirage Net.

{% embed url="https://github.com/MirageNet/Mirage" %}

#### Transport

{% hint style="danger" %}
This transport is **NOT** compatable with Heathen's Steamworks.

This is provided for informational purposes only. You may be able to use this infromation to port the Mirage Net Steam Transport to work with Heathen's Steamworks or to port the Mirror Transport to work with Mirage Net.

Heathen Engineering does not provide support for either of these two use cases. **This is wholly for informaitonal purposes only.**
{% endhint %}

Mirage Net is known to have a Steam Networking Transport based on the Fizzy Steam transport from Mirror. This transport however has not been updated with Heathen's contributions and so has the following major issues

1. It does not make proper use Steam Game Server APIs
2. It depends on SteamManager
3. It is not compatable with all versions of Steamworks.NET and cannot be used with Heathen's Steamwroks tools

{% embed url="https://github.com/MirageNet/FizzySteamyMirror" %}

