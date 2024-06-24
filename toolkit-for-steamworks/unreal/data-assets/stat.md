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

# Stat

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Stats are a simple concept keyed on the `API Name` of the stat. You would have created the stat in your Steamworks Developer Portal and defined its `API Name` there. You can create a Data Asset to represent your stat in your game content making it easier to manage and work with that specific stat.

You can create a Data Asset in your project for each of your stats

## Create

To create a new Stat Instance select the type StatDataAsset.

<figure><img src="../../../.gitbook/assets/image (453).png" alt=""><figcaption></figcaption></figure>

## Configuration

Select the new stat asset data object and set the API Name to match the value you defined in you Steamworks Developer Portal for the stat.

<figure><img src="../../../.gitbook/assets/image (454).png" alt=""><figcaption></figcaption></figure>

## Use

To get started using the stat create a variable in your Blueprint of type Stat Data Asset and set the default value to the desired stat.

<figure><img src="../../../.gitbook/assets/image (455).png" alt=""><figcaption></figcaption></figure>

You can now drag off that variable to access features of the stat for reading and setting values.

<figure><img src="../../../.gitbook/assets/image (456).png" alt=""><figcaption></figcaption></figure>
