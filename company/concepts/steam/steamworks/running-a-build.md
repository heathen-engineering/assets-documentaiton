---
description: Building and running a Steam game
---

# Running a Build

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../">Guides and Tutorials</a></td><td><a href="../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../assets/physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../assets/ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

A typical Steam game is made dependent on the Steam client. This means that you must have Steam installed and running and logged in as a user that has access to the App Id your attempting to initialize as.&#x20;

### Build Testing

For proper build testing you should deploy your game to the Steam client preferably using the Content feature of [steamcmd.exe](https://partner.steamgames.com/doc/sdk/uploading) as found in the [Steam SDK](https://partner.steamgames.com/doc/sdk). You can set up test aka beta packages and add addition users for testing builds before the game its self is published live.

{% embed url="https://partner.steamgames.com/doc/store/testing#internal" %}
Setting up internal testers
{% endembed %}

### Dev Testing

While most dev testing is taken care of in Unity Editor you may also want to test a build without necessary bothering to upload it to Steam. To do this you \*\***must\*\*** include the [steam\_appid.txt](steam\_appid.txt.md) file in the root of the build.

## Troubleshooting

The following sections are just to help people find this information when searching in the Knowledge Base ... they all just point you to [steam\_appid.txt](steam\_appid.txt.md).

### Closes and relaunches from Steam

You ran your build without deploying it to Steam and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.

### Crash on Launch

You ran your build without deploying it to Steam and have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.

### Tries to download Spacewar

You ran your build without deploying it to Steam and are using App ID 480 and  have not used the [steam\_appid.txt](steam\_appid.txt.md) as required.
