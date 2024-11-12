---
description: Using Visual Studio for debugging
---

# 🪳 Debugging

<figure><img src="../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

{% embed url="https://www.youtube.com/playlist?list=PLReL099Y5nRdW8KEd59B5KkGeqWFao34n" %}

## Introduction

Visual Studio is able to step through your code line by line and let you view the internal state of memory and even make changes as it runs. This is the single most important feature for any programmer to learn to master. Aside from leveraging the tools available to you good design is critically important. Use Try/Catch blocks and in development builds log messages to insure debug logs are rich and meaningful.

## Visual Studio

Debugging using Visual Studio is incredibly simple, the video playlist above will give you a good overview of all the important features of debugging with Visual Studio. Note that you can mouse Visual Studio to a build and even debug builds not just in Unity Editor.

## Debug.Log

Unity has a built in log, in the Unity Editor the log shows in your "Console" and writes to a text file. For builds its available in the text file. Where the log file is located depends on the build platform

{% embed url="https://docs.unity3d.com/Manual/LogFiles.html" %}
Find your log file
{% endembed %}

You can use Debug.Log, Debug.LogWarning and Debug.LogError to write messages to this log.&#x20;
