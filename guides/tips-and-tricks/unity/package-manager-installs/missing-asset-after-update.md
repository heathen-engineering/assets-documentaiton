---
description: When Unity Package Manager gets it wrong
---

# Missing asset after update

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

You may notice that after you update some packages that the package seems to break or that the objects the pacakge defines seem to be missing. This is due to a bug with Unity Package Manager introduced early 2023 and seems to effect multiple versions of Unity.

The fix is very simple,

Right Click on the folder for the package in your Packages folder and select Reimport. This will force Unity to recompile that package's assets and everything will be working.

Follows is a step by step

## Updating a package

<figure><img src="../../../../.gitbook/assets/image (2) (5).png" alt=""><figcaption></figcaption></figure>

In this example I will update Heathen's Steamworks Complete from 3.0.9 to 3.0.11 in a Unity 2022.2.4f1 project.

<figure><img src="../../../../.gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>

I did so by simply clicking the Update button in the upper right of the Package Manager window

## Observing the issue

<figure><img src="../../../../.gitbook/assets/image (4) (5).png" alt=""><figcaption><p>Screen shot of my SteamSettings object ... see how the script is not loaded</p></figcaption></figure>

Next observe the issue, you can do this in lots of ways in short Unity wont be able to load anything from the Package ... in this case I have selected a SteamSettings scriptable object and as you can see the inspector for it is empty.

## The Fix

To fix this simply right click on the Steamworks Complete folder in the Packages folder. and select Reimport

<figure><img src="../../../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

Once you click that Unity will recompile the related assemblies and all will work.

<figure><img src="../../../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

Here I have selected the same SteamSettings scriptable object and you can see its now populated the inspector as expected
