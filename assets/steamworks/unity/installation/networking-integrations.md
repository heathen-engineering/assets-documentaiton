---
description: Use whatever you like
---

# Networking Integrations

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

{% hint style="info" %}
We do not author any networking solutions nor do we need to.\
\
We work with Steamworks.NET and help other developers work with Steamworks.NET to insure that we are all compatible with Steamworks.NET.\
\
Thus any networking asset you would like to use you can use without any consideration with regards to Heathen. If they support Steamworks.NET then it will simply work. If they do not then it will not this is not something for Heathen to do.
{% endhint %}

The following is a selection of known Networking HLAPIs it is not an exhaustive list (not all of them) and is not an endorsement of any of them. This is PURLY for informational purposes only.&#x20;

{% hint style="danger" %}
Heathen \*\***DOES NOT\*\*** provide support for Mirror or any other networking API you may be using. For support for those APIs please contact those API's developers.
{% endhint %}

## Networking Integrations

Heathen Engineering works with the communities of other assets and tools to help insure a smooth and efficient integration between our technologies. In particular Heathen has invested notable effort in the networking transports of the following solutions and works to insure they function properly with the Steamworks.NET APIs and with our own Steamworks tools.

We however are not the author of these networking solutions and we do not take responsibility for the good working order of other peoples assets. If you have issues or need support for any of these or any other non-Heathen asset please contact the developer that created it for support.

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

Mirror is a community lead project based on Unity's abandoned uNET.&#x20;

Mirror has various transports including a Heathen compatible Steam Networking and Steam Sockets transport. Heathen Engineering does not author this transport but does contribute to its ongoing maintenance insuring proper use of the Steam APIs and compatibility with Heathen's Steamworks assets.

{% embed url="https://assetstore.unity.com/packages/tools/network/mirror-129321" %}

{% embed url="https://github.com/vis2k/Mirror" %}

#### Requirements

You must install the base of Mirror first, this can be done either from the Unity Asset Store via the Unity Package Manger or via GitHub.

#### Transports

{% embed url="https://github.com/Chykary/FizzySteamworks/" %}

Mirror Community's FizzySteamTransport has been made compatible with our asset and has been updated to support Peer to Peer and Client Server based networking architectures. The steps to install it are as follows.

**To install FizzySteamworks**

1. Open Unity 2020 LTS (latest build) or a more recent version of Unity preferably an LTS release
2. Open the Unity Package Manager
3. Click the "+" (plus) button located in the upper left of the window
4. Select the "Add package from git URL..." option\
   <img src="../../../../.gitbook/assets/image (144).png" alt="" data-size="original">
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
   <img src="../../../../.gitbook/assets/image (144).png" alt="" data-size="original">
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
   <img src="../../../../.gitbook/assets/image (144).png" alt="" data-size="original">
5. Enter the URL below and press the add button:

```
https://github.com/Unity-Technologies/mlapi-community-contributions.git?path=/Transports/com.community.netcode.transport.steamnetworking
```

##
