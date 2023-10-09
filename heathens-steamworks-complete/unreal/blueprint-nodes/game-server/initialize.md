---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
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

# 🔵 Initialize

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
Only valid for Steam Game Servers
{% endhint %}

Initializes the ISteamGameServer interface object, and set server properties which may not be changed.

After calling this function, you should set any additional server parameters, and then call [Log On](log-on.md) or [Log On Anonymous](log-on-anonymous.md)

### IP

The address of the server

### Game Port

The port that clients will connect to for gameplay.

### Query Port

The port that will manage server browser-related duties and info pings from clients.

### Mode

The authentication mode of the server

### Version

The version string is usually in the form `<Major>.<Minor>.<Build>.<Revision>`, and is used by the master server to detect when the server is out of date.

### Return Value

True if successful

## Nodes

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
