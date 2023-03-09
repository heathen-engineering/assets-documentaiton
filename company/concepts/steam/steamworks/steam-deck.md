# Steam Deck

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../">Guides and Tutorials</a></td><td><a href="../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../assets/physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../assets/ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% embed url="https://store.steampowered.com/steamdeck" %}
Store Page
{% endembed %}

{% embed url="https://partner.steamgames.com/doc/steamdeck" %}
Developer Documents
{% endembed %}

Steam Desk is a hand held Linux PC running (by default) Steam OS and design with Steam's "Big Picture" in mind. More than just a handheld Steam machine the Steam Deck product includes services that deal with verifying that games run well "On Deck".&#x20;

{% embed url="https://partner.steamgames.com/doc/steamdeck/compat#DeckCompatibilityChecklist" %}
Compatability Checks and Review Process
{% endembed %}

## Debugging with Unity

{% embed url="https://partner.steamgames.com/doc/steamdeck/testing" %}
Read Me
{% endembed %}

> _From Valve Documentation:_\
> Updating and downloading builds from Steam is not a great way to iterate, so we’ve created some software to help with this. That said, to use this software you will need to have a Linux test machine that’s separate from your dev PC.\
> \
> What we’ve made available is the SteamOS Dev Kit Client and SteamOS Dev Kit Service. These tools are now free to download on Steam. With these tools you’ll be able to upload builds, grab logs and traces, debug your build, and overall iterate much quicker than trying to work entirely through the SteamPipe.\
> \
> All you'll need to do is download the SteamOS Dev Kit Client to your development PC, download the SteamOS Dev-Kit Service to your Linux box, start them both up, and connect your PC to your Linux box. You can find links to download and learn how to use these tools [here](https://partner.steamgames.com/doc/steamdeck/loadgames).

### Unity Profiler

{% hint style="info" %}
Tips contributed by the [Heathen Development Community](https://discord.gg/6X3xrRc).
{% endhint %}

Connect the Unity Profiler via LAN. To do so in your build settings select and toggle on the Development Build and Autoconnect Profiler options.

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

In your profiler use the Attach to Player drop down and enter the IP Address of your Steam Deck

<figure><img src="../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
