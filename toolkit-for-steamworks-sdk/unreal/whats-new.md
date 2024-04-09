---
cover: ../../.gitbook/assets/Unreal Banner.jpg
coverY: -27
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

# What's New!

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Heathen has not stopped updating, improving, expanding and enriching its tools and knowledge base in over a decade ... and we aren't about to stop now!

This article describes major recent and upcoming changes coming to Heathen's Toolkit for Steamworks SDK for the Unreal Engine. GitHub Sponsors and Patreon Subscribers have access to all our changes as they occur as well as track and manage issues, feedback and suggestion tools. Becoming a sponsor is the best way to experience and guide the ongoing development of all of Heathen's great tools for all engines.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h3>GitHub Sponsor</h3></td><td><p><a href="https://github.com/sponsors/heathen-engineering">Become a Sponsor</a></p><p><em>The link below only works for Sponsors</em><br><a href="https://github.com/heathen-engineering/SourceRepo">Installation Instructions</a></p><p><em><mark style="color:yellow;"><strong>Cancel anytime, and keep everything you have including our site-based license</strong></mark></em></p><ul><li>$15.00 month</li><li>Source Access<br>For all our assets</li><li>Live Updates</li><li>Exclusive extras</li><li>Issue Tracking</li><li>Escalated Live Support</li><li><p>Unity</p><ul><li>Toolkit for Steamworks</li><li>PhysKit Complete</li><li>UX Complete</li></ul></li><li><p>Unreal</p><ul><li>Toolkit for Steamworks</li></ul></li></ul></td><td></td></tr><tr><td><h3>Unreal Marketplace</h3></td><td><p><a href="https://www.unrealengine.com/marketplace/en-US/product/ad658ddf5c434478acb95f9091ea279c">Unreal Marketplace</a></p><ul><li>$74.99</li><li>Source Included</li><li>Quarterly Updates<br>+ Hotfixes</li><li>Toolkit for Steamworks</li><li>Live Support</li></ul></td><td><mark style="color:orange;">Per-user license, free updates for that major version, discount on future major updates</mark></td></tr></tbody></table>

## What's New!

Version 2 introduces a dependency on Epic Games's Steam Shared plugin. This change means that Heathen's tools are now completely compatible with all of Epic's tools as well as any 3rd party tool built on them.

Version 1 was spawned from an internal tool and was a complete manual integration of Steamworks SDK. The advantage here was zero dependencies on anything from Epic the intent of that being to insure complete use and availability of Steamworks SDK without anything getting in the way. The disadvantage was an incompatibility with anything from Epic, this meant working with any existing tools, guides, features, etc. was harder and required more effort from the programmer.

Version 2's approach is to author our tools to work with any relevant version of the engine or Steamworks SDK and handle integration through common/shared Unreal Engine features such as Steam Shared. The net result of this change is that all existing tools, plugins, samples, tutorials, etc. around Unreal's Steamworks will simply work and that all of Heathen's "full feature set" will also simply work.

## v2 Changes

### Installation

v2 is dependent on the Steam Shared plugin\
When installing from Marketplace this will be enabled for you\
When installing it to a project you should enable Steam Shared yourself before adding the plugin.\
As Steam Shared is the base Steamworks SDK integration its rules apply in terms of configuration of App ID and similar. Please see our [Getting Started](getting-started.md#configuration) documentation for more information.

#### Prior Version

v1 contained a deep copy of Steamworks SDK and held all of its configuration internally exposing it to the Steam Game Instance class defaults. This meant you could install and configure the tool entirely "in the editor"

### Multiplayer

v2 is compatible with Unreal's Steam Sockets NetDriver and this is the tool you should use if you want to use Steam Networking Sockets.

{% hint style="info" %}
No, you do not have to use Online Subsystem, it is a technical dependency and will be enabled but does not have to be used. See the [Sockets Net Driver](sockets-net-driver.md) article for more information.
{% endhint %}

When you enable the Steam Sockets plug-in from the Plugins list in Unreal it will require a restart and there is some configuration you need to do in your ini files. See our [Sockets Net Driver](sockets-net-driver.md) article for more information.

#### Prior Version

The prior version used a modified Sockets Net Driver based on Epics built-in one. It has some known issues and a similar configuration, Those issues are not present in v2.&#x20;
