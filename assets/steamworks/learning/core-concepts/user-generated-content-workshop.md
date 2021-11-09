---
description: >-
  Deliver player mods, walkthroughs and more with Steam's User Generated Content
  System
---

# User Generated Content (Workshop)

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

{% hint style="success" %}
WIP



This page will discribe the features and use of Steam APIs remote storage tools and how might use that feature in practical sitautions.
{% endhint %}



The User Generate Content (UGC) API from Valve is used for a number of features including Leaderboard Details. This section of the Heathen Knowledge Base however deals with the use of UGC for Workshop files.

The typical use case is that you enable your users and or you yourself create workshop files (aka mods) and upload them to Valve's Workshop. These can then be browsed for and subscribed to by players. The system will then download the content that belongs to the subscribed mods and make that available to your game.

## Concepts

### Item File

This is not a single "file" such as a word.doc or folder.zip, instead this is an ID that represents a collection of content on the Steam UGC system and can be browsed for via the Steam Workshop interface. A given Workshop "file" may contain many files, it will have at least a description, name and preview image.

### Content Folder

When you create a new UGC item e.g. Workshop entry, you provide several bits of information including a "Content Folder Path". The files in this folder path will be collected by the Steam client, compressed and uploaded to Steam. You **should not** include compressed files such as zip or rar.&#x20;

### Subscription

As with DLC, Apps and Games, when Valve says you are "subscribed" to a thing it means that you have access to it. In the case of Workshop this means its been selected by the user and is or will be downloaded to the user's machine and keep up-to date.

### Browse the Workshop

While the typical use case is that the user would browse for items in the Steam Client, and this would be Heathen's recommendation as well, the Steam Client's UI is going to be duty built for the task where your game's UI is not.&#x20;

It is however possible to browse the workshop in game and Heathen's Steamworks SDK provides a number of tools to help you with this.

#### Workshop Browser

Heathen Engineering has created a simple UI Control named `WorkshopBrowser` which is demonstrated in the Workshop sample scene. This control handles searching for and browsing Workshop items and displaying them to the user along with similar controls to that found in the Steam Client e.g. favorites, subscribe, etc.

The control uses an item template making it easy to customize the appearance of each entry.

#### WorkshopItemQuery

The WorkshopBrowser uses the WorkshopItemQuery and SteamSettings.UGC interface to perform all of its actions. You can use these same tools to create a completely bespoke (custom) browser experience. Full source is provided with all Heathen Engineering assets so you can use the Workshop Browser as a working example.

