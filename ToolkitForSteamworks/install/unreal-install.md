# Unreal Install

## How to Install

<details>

<summary>GitHub Sponsor | Patreon</summary>

We strongly recommend you clone the repository to your local disk. The simplest way to do this is to use [GitHub Desktop](https://desktop.github.com/). Once you have that installed, you can easily clone any repository to your local disk.

<figure><img src="../.gitbook/assets/image (228).png" alt=""><figcaption></figcaption></figure>

Once you have the repository cloned to your local disk you need to locate the proper Plugin package for your engine version

<figure><img src="../.gitbook/assets/image (232).png" alt=""><figcaption></figcaption></figure>

Next, copy the ToolkitSteamworks folder into your Plugins folder. You may need to create the Plugins folder if this is the projects first plugin.

<figure><img src="../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure>

**Modify the Plugin configuration**

If you do not own the Plugin from the Unreal Marketplace then the Epic editor will see that this plugin is also a Marketplace plugin and expect you to download it from there

<figure><img src="../.gitbook/assets/image (234).png" alt=""><figcaption></figcaption></figure>

Modify the SteamworksComplete.uplugin to empty the `MarkeplaceURL` node, as shown below if you have this issue, you can skip this if its not an issue for you.

Copy

```
{
    ...
    "MarketplaceURL": "",
    ...
}
```

**Generate files**

Next, right-click on the .uproject file and select Generate Visual Studio project files

<figure><img src="../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

Right-click on your projects .uproject file and select `Generate Visual Studio Project files`. This will cause the engine to scan the project directory and link up all the related bits we just copied in.

</details>

{% hint style="warning" %}
FAB, unfortunately, cannot be updated and maintained properly due to limitations with Epic's FAB Marketplace tools. \
\
If you purchased on FAB, we will provide you with direct support and updates until which time Epic updates and improves the FAB Marketplace. Please contact us on our [Discord](https://discord.gg/9D8xJXYnF8) for more information.
{% endhint %}

## Samples

The plugin includes content such as a sample scene, which demonstrates all core features of the Toolkit for Steamworks SDK (Unreal).

<figure><img src="../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

If you dont see the Content folder in your Plugins, the most likely issue is that your Content Browser is not set to display Plugin Content, to change thi,s click the ![](<../.gitbook/assets/image (195).png>) button and select Show Plugin Content.

<figure><img src="../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

You can now see and run the Example scene, which demonstrates many common features, including&#x20;

* User Info
* Friends List
* Leaderboard
* Lobby
* Multiplayer Networking

<figure><img src="../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>

Multiplayer Networking works independently of the lobby; the "host" can simply click the "Listen" button. The connecting "client" should enter the "host"'s My ID: value after that. This is not here to demonstrate using a Steam Lobby to matchmaking, it's meant to be a bare bones connect 2 machines example using Unreal's built-in ThirdPersonMap or another stock sample scene that can support multiplayer.

Do note that Unreal will only initialise the Steam Socket plugin when run in Standalone.
