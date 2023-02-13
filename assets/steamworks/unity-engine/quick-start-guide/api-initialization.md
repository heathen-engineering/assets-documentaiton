# API Initialization

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Initialize Steam API with Heathen's API wrapper. This is the simplest method in terms of steps to perform but requires the most understanding and code from you while also giving you the most amount of control over the process.

Simply use the [API.App.Client.Initialize(...)](../../api/app.md#initialize) or the [API.App.Server.Initialize(...)](../../api/app.server.md#initialize) method. For client builds you would obviously use the Client version and for Server builds you use the server version. The articles linked for each will explain each method in more detail.&#x20;

## Steam Game Server

When working with the Steam Game Server API there are two stages to making the API ready for use.

1. Initialize the Steam API ... which is done via the [API.App.Server.Initialize(...)](../../api/app.server.md#initialize) method
2. Log the server on ... which is done via the [API.App.Server.LogOn()](../../api/app.server.md#logon) method

Note that you can configure automatic logon in the [Steam Game Server Configuraiton](../../objects/steam-game-server-configuration.md) object you pass into the Initialize method. This will instruct our system to "log on" as soon as initialization is complete.
