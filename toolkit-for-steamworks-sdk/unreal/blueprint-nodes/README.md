---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Blueprint Nodes

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

See the navigation panel to the left to browse all available nodes.

In Unreal Blueprint editor you can search for nodes by simply typing the node name. All Steamworks Complete nodes start with "Steam" so you can simply type "Steam" to see a list of all possible nodes.

In Unreal we have organized the nodes into categories similar to but not limited to the related Steam API interface e.g. Steam App, Steam Friends, etc. In all cases, node functions will return a default empty value if Steam is not yet initiated.

To simplify node use in Unreal Blueprints we have devolved the Steamworks data types to their respective Blueprint-suitable primitives.&#x20;

### Examples

* CSteamID --> int64
* AppId\_t --> int32
* AccountId\_t --> int32
* CGameID --> int64

Unreal blueprints do not play nice with unsigned values but Valve expects unsigned values as a result it is up to you to ensure you never pass a value less than zero, the results will be undefined if you do.

In cases where Steam API would work with a char\[] or Linux epoch time we have converted these to the appropriate Blueprint-friendly Unreal-type

### Examples

* Steam int64Time --> FDateTime
* Steam char\* --> FString
