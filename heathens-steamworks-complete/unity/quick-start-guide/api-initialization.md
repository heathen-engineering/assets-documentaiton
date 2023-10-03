---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
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

# API Initialization

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Initialize Steam API with Heathen's API wrapper. This is the simplest method in terms of steps to perform but requires the most understanding and code from you while also giving you the most amount of control over the process.

Simply use the [API.App.Client.Initialize(...)](../api/app.client.md#initialize) or the [API.App.Server.Initialize(...)](../api/app.server.md#initialize) method. For client builds you would obviously use the Client version and for Server builds you use the server version. The articles linked for each will explain each method in more detail.&#x20;

## Steam Game Server

When working with the Steam Game Server API there are two stages to making the API ready for use.

1. Initialize the Steam API ... which is done via the [API.App.Server.Initialize(...)](../api/app.server.md#initialize) method
2. Log the server on ... which is done via the [API.App.Server.LogOn()](../api/app.server.md#logon) method

Note that you can configure automatic logon in the [Steam Game Server Configuraiton](../objects/steam-game-server-configuration.md) object you pass into the Initialize method. This will instruct our system to "log on" as soon as initialization is complete.
