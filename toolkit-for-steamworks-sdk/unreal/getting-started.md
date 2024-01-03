---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Getting Started

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## [Installation](installation.md)

Import the Toolkit for Steamworks plugin to your project. Whether you purchased the plugin from Unreal Marketplace or are a GitHub Sponsor you will need access to the Toolkit for Steamworks plugin to get started using it.

The plugin is not free and is only available from Heathen via the [GitHub Sponsor](../../become-a-sponsor/) program and on the [Unreal Marketplace](https://www.unrealengine.com/marketplace/en-US/product/ad658ddf5c434478acb95f9091ea279c). If you acquired the plugin anywhere else we suggest you remove it immediately as it's not a legit copy and likely contains malware.&#x20;

## [Game Instance](game-instance.md)

With the plugin installed, you will want to set up your Game Instance.&#x20;

The plugin ships with a ready-to-use Steam Game Instnace named `BP_Steam_Game_Instance` You can use this as is or use it as a learning tool to create your own Game Instnace derived from our SteamGameInstance parent class or use it as is.

## [Steam Developer](../../company/steam/quick-start.md#sign-up-to-steamworks)

Become a Steam Developer and get your own App ID.

Valve does provide a test app ID you can use as a matter of demonstration and our Steam Game Instance will default to its App ID (480) however you will want to register for your own App ID as soon as possible.

You can learn more about [getting started as a Steam Developer in our article here](../../company/steam/quick-start.md)!

## Use the kit

The Example Level presents a UI that demonstrates key features

<figure><img src="../../.gitbook/assets/image (391).png" alt=""><figcaption></figcaption></figure>

Be sure to check out the Graph on the BP\_Example\_UI for additional examples such as how to find, join and create a Steam Lobby, Host and Join a network session via Steam Networking Sockets, etc.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Beyond samples we have extensive documentation including how-to guides for nearly every aspect of the Steam platform, going beyond simple documentation for our tools and assets. You can learn more about all the features of Steam in our knowledge base by reviewing the hundreds of articles linked in the navigation panel to the left 👀

<figure><img src="../../.gitbook/assets/image (371).png" alt=""><figcaption></figcaption></figure>

If you have any questions simply look up ... there you will find our Search tool which is AI-assisted and fairly useful as well as links to our [Discord Community](https://discord.gg/6X3xrRc) where you can get live support.

## Troubleshooting

### Editor Fails to Load

When you first install/enable the plugin whether you installed it as a Project Plugin or Engine Plugin you may get a message similar to&#x20;

<figure><img src="../../.gitbook/assets/image (386).png" alt=""><figcaption></figcaption></figure>

This is caused when the editor cannot find the required assemblies and is typically corrected with a Clean and Rebuild. If Clean and Rebuild does not resolve the issue check the Binaries folder of the Plugin and ensure that the Encrypted App TIcket and Steam API assemblies are present.

<figure><img src="../../.gitbook/assets/image (387).png" alt=""><figcaption><p>Shows the assemblies as used by Widnows </p></figcaption></figure>

If you need to locate a copy of these assemblies to manually access you can find them at the paths listed below.

#### Steam API Assemblies

`Plugins\SteamworksComplete\Source\ThirdParty\SteamworksCompleteLibrary\sdk\redistributable_bin`

Each platform has a sub-folder

#### Encrypted App Ticket

`Plugins\SteamworksComplete\Source\ThirdParty\SteamworksCompleteLibrary\sdk\public\steam\lib`\`

Each platform has a sub-folder&#x20;

### Package Fails to Load

As with the editor, this is caused by the required assemblies not being copied over correctly during the packaging process. You can confirm this by reviewing the Binaries folder

<figure><img src="../../.gitbook/assets/image (388).png" alt=""><figcaption><p>Shows the required assemblies for a Windows build</p></figcaption></figure>

If you need to locate a copy of these assemblies to manually access you can find them at the paths listed below.

{% hint style="info" %}
You can also copy them from the Binary folder of the Plugin in your project. This is where the Unreal Editor should have copied them from.
{% endhint %}

#### Steam API Assemblies

`Plugins\SteamworksComplete\Source\ThirdParty\SteamworksCompleteLibrary\sdk\redistributable_bin`

Each platform has a sub-folder

#### Encrypted App Ticket

`Plugins\SteamworksComplete\Source\ThirdParty\SteamworksCompleteLibrary\sdk\public\steam\lib`\`

Each platform has a sub-folder&#x20;

### Package Closes/Crashes on launch

This happens when you run a package that has not been deployed by the Steam client. You will find that the Should Restart event if you simply copied the example implementation closes the app if it has not been launched from the Steam client.

[See more here.](game-instance.md#should-restart)

You can prevent this check by adding a steam\_appid.txt to the root of your project as shown in the image below

{% hint style="warning" %}
DO NOT ship your game with steam\_appid.txt this bypass is meant for devs.

You DO want your game to shut down and relaunch from the Steam client to ensure the Steam API works properly in every other use case.

[Learn more about steam\_appid.txt and when to and when not to use it.](../../company/steam/steamworks/steam\_appid.txt.md)
{% endhint %}

<figure><img src="../../.gitbook/assets/image (389).png" alt=""><figcaption></figcaption></figure>

### Callbacks not working in the package

In most cases, this is due to Steam API not initializing,&#x20;

In most cases, with a package, this is due to you running the package without deploying it from the Steam client without using the steam\_appid.txt and without properly handling the [Restart Required](game-instance.md#should-restart) case.

When you run the package Steam API will perform a check known as "Restart Required" This checks to see if the app was run from the Steam client, if it was not it will attempt to re-launch the game from the Steam client.

If you are just getting started however your game won't have launch options in the Steam client so that will do nothing.

In addition, Steam API will not have initialized and will not be processing callbacks e.g. Steam API is simply not working in that case.

You can sidestep the Restart Required check by using the [steam\_appid.txt](../../company/steam/steamworks/steam\_appid.txt.md), please read and understand what steam\_appid.txt is before you use it.

### On Launch 2 Windows Open

You are running your package without having deployed it from the Steam client.

You have configured launch options for your app

You are not handling the [Restart Required](game-instance.md#should-restart) case properly.

When you run the package Steam API will perform a check known as "Restart Required" This checks to see if the app was run from the Steam client, if it was not it will attempt to re-launch the game from the Steam client.

In addition, Steam API will not have initialized and will not be processing callbacks e.g. Steam API is simply not working in that case.

You can sidestep the Restart Required check by using the [steam\_appid.txt](../../company/steam/steamworks/steam\_appid.txt.md), please read and understand what steam\_appid.txt is before you use it.
