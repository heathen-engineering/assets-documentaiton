---
description: Known issue and how to sort them
---

# ⚠️ Known Issues

## 'NamedBuildTarget' does not exist

### Issue

* Identified on Unity v6000.0.25f1 and later this appears to be a change on Unity's side that causes a script in Steamworks.NET to not compile correctly.&#x20;

{% embed url="https://github.com/rlabrecque/Steamworks.NET/issues/654" %}

### Workaround

You can work around this by double-clicking the error and adding&#x20;

```csharp
using UnityEditor.Build;
```

To the using statements, this will update your cache copy of Steamworks.NET so you will need to do this again if you Update that plugin assuming its author hasn't fixed it yet.&#x20;

## Steamworks.NET for Steamworks SDK v1.60

{% hint style="info" %}
This does affect the version that is installed by default e.g. the latest version of Steamworks.NET
{% endhint %}

### Issues

* Steam Deck won't Initialize Steamworks SDK\
  Steamworks.NET for Steamworks SDK version 1.60 has a known issue which causes problems initializing Steamworks on some versions of Steam Deck.

{% embed url="https://github.com/rlabrecque/Steamworks.NET/issues/647" %}

* Achievements don't work / Import\
  Steamworks.NET for Steamworks SDK version 1.60 has a known issue which causes Steam Achievements, Stats and similar to intermittently work. This generally manifests as not being able to import Achievements from Steam or not being able to set or unlock achievements or stats.

{% embed url="https://github.com/rlabrecque/Steamworks.NET/issues/650" %}

### Workaround

{% hint style="info" %}
This workaround doesn't always work, we are thus adding a more forceful way to get around the import issue with 2025 and later. You can select the Steam Settings object in your Settings folder and manually add Achievement objects to it

You will see a new text field beside the Import button, you can enter a name and when you do an Add button will appear clicking that will add the Scriptable Object.\
![](<../../.gitbook/assets/image (479).png>)

Ideally, you would avoid doing this, in this manner as it is not as easily maintained as imported values or using the AchievmentData struct in C# directly. It can however help you work around this issue until Valve or Steamworks.NET corrects the problem.
{% endhint %}

Use Steamworks.NET for Steamworks SDK version 1.59

{% hint style="danger" %}
DO NOT USE STEAMWORKS.NET 20.0 OR SIMILAR THAT IS FAR TO OLD&#x20;
{% endhint %}

You DO want to use Update to Steamworks SDK 1.59 which you can access via GitHub History

{% embed url="https://github.com/rlabrecque/Steamworks.NET/tree/078ed3c7c9b767a42be555b75ea5fb014c067132/com.rlabrecque.steamworks.net" %}

To save you time and reading ... you can just click the link below it will download a zip from GitHub containing the historical state of Steamwroks.NET during the 1.59 patch that you can then install via Unity Package Manager as "Add from Disk"

{% embed url="https://github.com/rlabrecque/Steamworks.NET/archive/078ed3c7c9b767a42be555b75ea5fb014c067132.zip" %}

It will download a zip containing Riley's repo during his 1.59 update before this issue was introduced but after the security patch for initialization and authentication changes
