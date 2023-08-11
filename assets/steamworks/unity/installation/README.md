---
description: Installing Heathen Engineering's Steamworks and related componenets.
---

# Installation

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

How you install depends on how you chose to license Heathen's Steamworks. The following cards cover the installation instructions and core features of each of the three major ways to license Heathen's Steamworks.

{% hint style="danger" %}
Make sure you do not have a "deep copy" of Steamworks.NET in your project. If you do have a copy then Unity will attempt to merge it and issues will occur.\
\
Unfortunately, some other Steamworks-related assets do have a full copy of Steamworks.NET embedded in the asset package. This will cause numerous issues for you.\
\
You may have also imported Steamworks.NET from GitHub via a .unitypackage and this will cause you issues.\
\
Steamworks.NET should only be installed via the Unity Package Manager. Our asset will import Steamworks.NET via the Unity Package Manager for you, or you can import it via the Add from Git URL option in Unity Package Manager.\
\
This insures the following important factors

* You have the latest code from GitHub\
  If you import the .unitypackage from the releases folder it is usually out of date sometimes by a significant amount. Installing from the Package Manager pulls directly from the source and is always live and up-to-date
* The assembly can be referenced\
  If you import via .unitypackage the Steamworks.NET assembly cannot be referred to as a compilation condition by other assets. This is a limitation of Unity's Assembly Dev such that only Packages can be referenced in this manner thus you need to install via the Package Manager
{% endhint %}



{% embed url="https://www.youtube.com/watch?v=vxZ0jvBi0s8" %}
Video is silent but does have subtitles/captions
{% endembed %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h3>Foundation</h3></td><td><p><a href="https://github.com/heathen-engineering/SteamworksFoundation/tree/main/Unity">Installation Instructions</a></p><ul><li>Free</li><li>Source Access</li><li>Limited Feature Set</li></ul></td><td>Package Manager Install</td></tr><tr><td><h3>GitHub Sponsor</h3></td><td><p><a href="https://github.com/sponsors/heathen-engineering">Become a Sponsor</a></p><p><em>Link below only works</em><br><em>for Sponsors</em><br><a href="https://github.com/heathen-engineering/SourceRepo">Installation Instructions</a></p><ul><li>$15.00 monthly</li><li>Source Access</li><li>Live Updates</li><li>Steamworks Complete</li><li>PhysKit Complete</li><li>UX Complete</li><li>Exclusive extras</li><li>Issue Tracking</li><li>Escalated Support</li></ul></td><td>Package Manager Install<br><br>Cancel anytime, keep everything you have includes site based license</td></tr><tr><td><h3>Unity Asset Store</h3></td><td><p><a href="https://assetstore.unity.com/packages/tools/integration/steam-api-steamworks-complete-246652">Buy Now</a><br>Installation Instructions</p><ul><li>$75.00</li><li>Source Included</li><li>Quarterly Updates<br>+ Hotfixes</li><li>Steamworks Complete</li></ul></td><td>Asset Store Install<br><br><mark style="color:orange;">Per-user based license, free updates for that major version, discount on future major updates</mark></td></tr></tbody></table>
