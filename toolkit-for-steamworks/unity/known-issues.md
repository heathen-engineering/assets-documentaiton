---
description: Known issue and how to sort them
---

# ⚠️ Known Issues

## Steamworks.NET for Steamworks SDK v1.60

### Issues

* Steam Deck won't Initialize Steamworks SDK\
  Steamworks.NET for Steamworks SDK version 1.60 has a known issue which causes problems initializing Steamworks on some versions of Steam Deck.

{% embed url="https://github.com/rlabrecque/Steamworks.NET/issues/647" %}

* Achievements don't work / Import\
  Steamworks.NET for Steamworks SDK version 1.60 has a known issue which causes Steam Achievements, Stats and similar to intermittently work. This generally manifests as not being able to import Achievements from Steam or not being able to set or unlock achievements or stats.

{% embed url="https://github.com/rlabrecque/Steamworks.NET/issues/650" %}

### Workaround

Use Steamworks.NET for Steamworks SDK version 1.59

{% hint style="warning" %}
DO NOT USE STEAMWORKS.NET 20.0 OR SIMILAR THAT IS FAR TO OLD&#x20;
{% endhint %}

You DO want to use Update to Steamworks SDK 1.59 which you can access via GitHub History

{% embed url="https://github.com/rlabrecque/Steamworks.NET/tree/078ed3c7c9b767a42be555b75ea5fb014c067132/com.rlabrecque.steamworks.net" %}

To save you time and reading ... you can just click the link below it will download a zip from GitHub containing the historical state of Steamwroks.NET during the 1.59 patch that you can then install via Unity Package Manager as "Add from Disk"

{% embed url="https://github.com/rlabrecque/Steamworks.NET/archive/078ed3c7c9b767a42be555b75ea5fb014c067132.zip" %}

It will download a zip containing Riley's repo during his 1.59 update before this issue was introduced but after the security patch for initialization and authentication changes
