---
description: When you need it on-demand
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Steamworks Event Triggers

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The Steamworks Event Triggers component works similarly to Unity's Event Trigger component letting you easily connect to any Steamworks SDK static event quickly and easily. There is no reason to use this component in C# code as all of these events are available on their respective API extensions. This component exists only to expose those events to the Unity Inspector.

## Use

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Simply click the Add New Event Type and select the event you wish to add

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

When done you can connect objects to the event as you would any other Unity Event. You are not required to use this component to access these events. Each event is also available on related "Managers" such as the [Lobby Manager](../ui-components/lobby-manager.md) as well as in code via the respective [API extensions](../api/).
