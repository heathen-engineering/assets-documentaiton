---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
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

# Testing

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This article outlines the testing methodology and processes to validate the good working order of Steamworks Complete. The [sample scenes](../sample-scene.md) serve as the core tests and are designed to be ran on a clean project configured for a Steam compatible platform (Windows, Mac or Linux) and for the Steam App 480 aka “Spacewars”.

The function of these tests are to insure the good working order of the asset independent of the unique conditions of a given project and to demonstrate the basic use of the core Steam API features.&#x20;

## Spacewars Tests

### Background

Spacewars also known as App 480 is a Steam app that all Steam users have access to and is used by Valve to demonstrate all major aspects of the Steamworks SDK and Steam API. The App can be used to prove the good working order of the basic functions of Steamworks without requiring the developer to secure Steam Partnership and a Steam App ID.

Spacewars has several limitations in that the developer will not have any access to Spacewars Developer Portal and is not listed as a “Steam Developer” of the app. As such Steam Inventory testing and control testing of Steam Workshop, Steam Leaderboard and Steam Input is not possible. To test these more advanced features the developer will need to secure there own Steam App ID and configure the related features in the Steam Developer Portal. Guides are provided in the Knowledge Base to that effect and notes are available (here) to help you create tests for those features.

### Methodology

Heathen has provided a set of sample scenes which exercise all major features of the Steam API. Each scene is “standalone” and can be ran in isolation to prove the basic functionality of that feature.

The expectations are:

1. The developer will set up a clean project configured for Windows, Mac or Linux standalone build.
2. They will import Heathen's Toolkit for Steamworks in the normal fashion (Unity Asset Store or GitHub Add from Disk or GitHub Add from Git URL).
3. That the project will remain free of customization or custom code as a “clean example” of the asset in isolation

These expectations allow the developer to review and compare the clean operation of Steamworks against the behaviour observed in a live project and thus can be used to identify and isolate the source of error as either Asset or Bespoke Code more quickly.

In addition, Heathen provides an in-editor window “[Steamworks Inspector](./)” available in the \[Windows > Steamworks > Inspector] menu that can be used to inspect and exercise all major Steamworks features. For more information on the Steamworks Inspectors please read the [Knowledge Base article](./). The Steamworks Inspector works with any App as long as Steamworks API is initialized (you are running the app in the editor).

### [Sample Scenes](../sample-scene.md)

Note for GitHub Sponsors installing the asset from Unity Package Manager you will need to import the samples from the Sample dropdown in the Package Manager. Please read [this article](../sample-scene.md) for more information.

Each sample scene describes the objects in the scene, their use and the expected results. The Unity Editor Console log will provide details as to each step of the operation along with highlighting any errors or warnings in such a manner that they can be easily reported.

{% hint style="success" %}
Want to share your Unity consoler log?\
\
Select the Console log item you want to share in Unity Editor\
Press \[Ctrl + C] This will copy the whole message including its stack to your clipboard\
You can now paste that into Discord, email or elsewhere ... far better than a screenshot or video.
{% endhint %}

