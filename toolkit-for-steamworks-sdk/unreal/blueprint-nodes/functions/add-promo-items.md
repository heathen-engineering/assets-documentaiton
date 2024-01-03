---
cover: ../../../../.gitbook/assets/Unreal Banner@2x.png
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

# 🔵 Add Promo Items

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Grant specific one-time promotional items to the current user.

This can be safely called from the client because the items it can grant can be locked down via policies in the itemdefs. One of the primary scenarios for this call is to grant an item to users who also own a specific other game. This can be useful if your game has a custom UI for showing a specific promo item to the user otherwise if you want to grant a single promotional item then use [AddPromoItems](https://partner.steamgames.com/doc/api/ISteamInventory#AddPromoItems).

Any items that can be granted MUST have a "promo" attribute in their itemdef. That promo item lists a set of APPIDs that the user must own to be granted this given item. This version will grant all items that have promo attributes specified for them in the configured item definitions. This allows adding additional promotional items without having to update the game client. For example, the following will allow the item to be granted if the user owns either TF2 or SpaceWar.

```json
promo: owns:440;owns:480
```

## Options

Heathen provides two options when working with this endpoint.

### Simple

Our Simple variant will save you a lot of effort by handling the result-ready event for you, processing any requested properties and handing you a completed collection of item details when it's all done.

With the simple method, you should provide the item you wish to add as well as any properties you would like us to read from the resulting item. In most cases you won't need additional properties read however if your items have generators on them that create custom properties on creation then you may want to have us read those for you

#### Item Defs (input)

The items to grant the player

#### Read Properties (input)

An array of strings being the keys for each property you would like us to read for you

#### Callback (input)

The callback is an event that will contain the [UEResult](../enumerators/ueresult.md) of the request and an array of [Item Detail With Properties](../types/item-detail-with-properties.md)

#### Return Value

Always true when called by a regular user, always false when called by a Steam Game Server.

### Example

<figure><img src="../../../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

Note that we never return the result handle to you, we track this handle, process the items, read the requested properties and destroy the handle for you returning to you the resulting data in an array.

### Native

The native Steam API works by issuing the request and returning an Item Request Handle when the request is filled Steam will execute the Result Ready callback. You must then read the details, properties and other aspects you desire from the result and then destroy the result handle.

### Item Defs (input)

The definition ID of the items to grant the player.

### Example

To get the handle you make your request, and check if the request was successful, if so store that request ... you'll need the handle from it later. This will prompt Steam to execute the Result Ready event when the results have been read.

<figure><img src="../../../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

When the Result Ready is executed you will need to check if it matches your result handle, fetch the items contained in that result, and for each item fetch whatever additional properties you may need.

<figure><img src="../../../../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure>

Importantly when you are done reading the data returned by that result you need to destroy the handle.

<figure><img src="../../../../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>
