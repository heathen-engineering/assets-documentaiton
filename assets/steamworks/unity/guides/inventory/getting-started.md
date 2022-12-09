---
description: >-
  Getting started with Steam Inventory via Heathen Engineering's Steam Inventory
  Manager tools
---

# Getting Started

<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
You cannot test Steam Inventory features with App ID 480 aka Spacewars.

\
In order to test Steam Inventory features including but not limited to microtransactions, crafting, player inventory, etc. you will need to register your for your own app ID and configure your own Steam Inventory Items.\
\
As a result of this limitation from Valve the sample scenes for Inventory cannot be used with App 480 in any functional form.
{% endhint %}

First, you should understand what Steam Inventory is and is not, the only real place to do so is via Valve's documentation and videos on the feature.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/inventory" %}

You will also need to understand the Steam Inventory Schema, while Heathen's tools help you define your item definitions in this schema there will be time when you need to manually edit to take advantage of more complex features, or to apply some unique concept specific to your project.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

## **Set up**

The hardest part about Steam Inventory is usually setting up your Steam Inventory Items. Have no fret Heathen is here to help!

The very first thing you should do is import any Steam Inventory Items you already have. You can do this quickly by simply running the simulation (so that Steam API is initialized) and clicking the Import button under the Inventory list in your Steam Settings

![](<../../../../../.gitbook/assets/image (187) (1) (1) (1) (1).png>)

Once done you will see every item you had defined already in your Steam Developer Portal has been pulled into Unity under your Steam Settings:

![Screen shot of a WIP project with 57 items. You can see here how the Settings object categorizes the items based on type.](<../../../../../.gitbook/assets/image (169) (1) (1) (1).png>)

## **Defining Items**

Creating new items is quick and easy simply click the "<mark style="color:green;">+ New</mark>" button in the Inventory list of Steam Settings and a new empty item will be created for you. Select that item and set the values as desired.&#x20;

Every Steam Inventory Schema feature is available but the inspector will hide ones that cannot be used with the currently selected type.

![Normal items can be traded, marketed, sold, etc.](<../../../../../.gitbook/assets/image (166) (1) (1) (1) (1) (1) (1).png>)

![Tag Generators only exist to attach to other items as generators](<../../../../../.gitbook/assets/image (177) (1) (1) (1).png>)

## **Uploading the Schema**

Once you have defined your items you can copy the JSON data that represents the item, or optionally copy all of the items to your clipboard and past the results into Steam Developer Portals item editor or into a text file to be uploaded later.

{% hint style="info" %}
You can find the Copy JSON button on the Inventory Item object and in the Inventory list of the Steam Settings object.

On the Steam Settings object it will export the JSON for every item in a single collection.

On the item it will export only that item's JSON
{% endhint %}

```json
{	
	"appid": 480,
	"items": [
		{
			"itemdefid": 1001,
			"type": "tag_generator",
			"name": "Example Tag Generator",
			"tag_generator_name": "Rarity",
			"tag_generator_values": "Common:75;Rare:20;Epic:5",
			"granted_manually": False	
		}]
}
```

Once you have your items you should upload them to the Steam Developer Portal as indicated in Valve's documentation. You are safe to edit the schema in its text form if you need/like you can always reimport them from Steam later.

## Using your items

Now that you have items defined in your Steam Developer Portal, and you have representations of those items in your Unity Project linked with your Steam Settings you can use Heathen's tools to manage the items at both dev time and run time.

{% hint style="info" %}
The Inventory Item Definitions stored in your Steam Settings object act as an inventory. See the [Inventory Item](../../scriptable-objects/item-definition.md) documentation for more information.
{% endhint %}

For developers needing to test, you can use the Steamworks Inspector to inspect, grant and clear items from your inventory. This is particularly useful since you can not use Steam client to view items for a game that is not yet released so the only way to view your items before release is to use our tool.

![](<../../../../../.gitbook/assets/image (159) (1) (1) (1) (1).png>)
