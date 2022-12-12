---
description: Understanding Steam DLC and the Heathen Engineering tool kit
---

# Downloadable Content

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% hint style="warning" %}
#### Understanding Steam DLC

Its important to understand the proper usage of DLC. Most of this is a matter of configuration in the Steam Developer Portal. Please carefully and fully read the documentation for the feature. It can be found here [https://partner.steamgames.com/doc/store/application/dlc](https://partner.steamgames.com/doc/store/application/dlc)
{% endhint %}

![](<../../../../.gitbook/assets/image (183) (1) (1) (1) (1).png>)

The [Downloadable Content Object](../scriptable-objects/downloadable-content-object.md) helps you track the status of DLC. You can import the DLC you have defined in the Steam Developer Portal for this application by running the simulation such that Steam API is able to initialize and then clicking the Import button on the Steam Settings Downloadable Content list

![](<../../../../.gitbook/assets/image (157) (1) (1) (1).png>)

Once completed all of the DLC registered to your application will be listed under your Steam Settings

![](<../../../../.gitbook/assets/image (178) (1) (1) (1) (1).png>)

And can be used to test ownership of the indicated DLC. Please see the [Downloadable Content Object](../scriptable-objects/downloadable-content-object.md) for details on the use of the object.
