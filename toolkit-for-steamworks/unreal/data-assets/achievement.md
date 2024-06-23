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
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Achievement

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Achievements are a simple concept keyed on the `API Name` of the achievement. You would have created the achievement in your Steamworks Developer Portal and defined its `API Name` there. You can create a Data Asset to represent your achievement in your game content making it easier to manage and work with that specific achievement.

You can create a Data Asset in your project for each of your achievements

## Create&#x20;

Create a new Data Asset Instance of type AchievementDataAsset

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption><p>Create a new Data Asset of type AchievementDataAsset</p></figcaption></figure>

## Configure

Set the API Name to the same value you defined in your Steamworks Developer Portal for this achievement.

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Set the API Name to match the name you set in Steamworks Developer Portal</p></figcaption></figure>

## Use

To use the achievement you can simply create a variable of type AchievementDataAsset and set its default value to be the instance you just created.

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Create a variable where required and select your Achievement as its Default Value</p></figcaption></figure>

With the variable set you can simply drag off that variable to access the functions and features of a Steam Achievements relative to this specific achievement.

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Use it as you see fit</p></figcaption></figure>
