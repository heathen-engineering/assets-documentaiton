---
description: When Unity Package Manager gets it wrong
---

# Missing asset after update

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../steam/">Guides and Tutorials</a></td><td><a href="../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../assets/physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../assets/ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

You may notice that after you update some packages that the package seems to break or that the objects the pacakge defines seem to be missing. This is due to a bug with Unity Package Manager introduced early 2023 and seems to effect multiple versions of Unity.

The fix is very simple,

Right Click on the folder for the package in your Packages folder and select Reimport. This will force Unity to recompile that package's assets and everything will be working.

Follows is a step by step

## Updating a package

<figure><img src="../../../.gitbook/assets/image (2) (5).png" alt=""><figcaption></figcaption></figure>

In this example I will update Heathen's Steamworks Complete from 3.0.9 to 3.0.11 in a Unity 2022.2.4f1 project.

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

I did so by simply clicking the Update button in the upper right of the Package Manager window

## Observing the issue

<figure><img src="../../../.gitbook/assets/image (4) (5).png" alt=""><figcaption><p>Screen shot of my SteamSettings object ... see how the script is not loaded</p></figcaption></figure>

Next observe the issue, you can do this in lots of ways in short Unity wont be able to load anything from the Package ... in this case I have selected a SteamSettings scriptable object and as you can see the inspector for it is empty.

## The Fix

To fix this simply right click on the Steamworks Complete folder in the Packages folder. and select Reimport

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Once you click that Unity will recompile the related assemblies and all will work.

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Here I have selected the same SteamSettings scriptable object and you can see its now populated the inspector as expected
