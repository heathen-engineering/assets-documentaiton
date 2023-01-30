---
description: A quick start guide for those already comfortable with the basics.
---

# Quick Start

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Initialization

Initializing the Steam API is the first step and you have a few choices on how you do this.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>Game Object</h3></td><td><ul><li>Zero Code</li></ul></td><td><a href="../../../../.gitbook/assets/Screenshot 2023-01-30 111452.png">Screenshot 2023-01-30 111452.png</a></td><td><a href="../../for-unity-game-engine/quick-start-guide/gameobject-initialization.md">gameobject-initialization.md</a></td></tr><tr><td><h3>Scriptable Object</h3></td><td><ul><li>No GameObject</li><li>Single line of code</li></ul></td><td><a href="../../../../.gitbook/assets/Screenshot 2023-01-30 111537.png">Screenshot 2023-01-30 111537.png</a></td><td><a href="../../for-unity-game-engine/quick-start-guide/scriptableobject-initialization.md">scriptableobject-initialization.md</a></td></tr><tr><td><h3>API</h3></td><td><ul><li>No GameObject</li><li>No ScriptableObject</li><li>Pure C#</li></ul></td><td><a href="../../../../.gitbook/assets/Screenshot 2023-01-30 111633.png">Screenshot 2023-01-30 111633.png</a></td><td><a href="../../for-unity-game-engine/quick-start-guide/api-initialization.md">api-initialization.md</a></td></tr></tbody></table>

## Networking

{% embed url="https://kb.heathenengineering.com/assets/steamworks/guides/multiplayer" %}

{% hint style="success" %}
Steamworks Complete and whatever HLAPI you chose to work with have no impact on each other at all. You will use Steamworks and your HLAPI of choice exactly the same with as you would without the other.
{% endhint %}

### Do I need Steamworks Complete?

You do **not** "require" Steamworks Complete in order to use Mirror, FishNetworking or NetCode for GameObject's or any other Steam transports. Those transports like our self work with Steamworks.NET directly.

That said you will need to initialize, configure and manage the Steam API before SteamNetworking interfaces can be used. Our Steamworks Complete and Steamworks Foundation packages make working with Steam API simple and stable. If you do not use Steamworks Complete or Foundation you would need to use the raw Steam API to initialize and configure your Steam API integration your self before your HLAPI could use the Steam transports.

### Examples?

Where can I find examples on using Steamworks Complete and (the HLAPI I chose)?

You cant because their is no need. Both Steamworks Complete and your HLAPI of choice work exactly the same rather or not the other exists. Thus we do not have an example of using (your HLAPI of choice) along side our Steamworks Complete.&#x20;

If you want to see an example of using your HLAPI of choice with your HLAPI's Steam transport then you should contact them. We have links to [Fish Networking, Mirror and NetCode for GameObjects in our articles](../installation/networking-integrations.md) but any HLAPI that works with Steamworks.NET properly will work.

If your looking for examples on how to initialize, configure and use Steam API (in general) you will find various samples in the provided [samples scenes](../../../physkit/learning/sample-scenes/) and examples throughout our knowledge base.

If your trying to wrap your head around creating a [multiplayer game on the Steam platform](broken-reference), we have an article for that as well. That article is not specific to any given HLAPI because the HLAPI you choose has no impact on the concepts involved.
