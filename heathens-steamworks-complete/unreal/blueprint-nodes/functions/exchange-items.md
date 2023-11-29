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

# 🔵 Exchange Items

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Grant one item in exchange for a set of other items.

This can be used to implement crafting recipes or transmutations, or items which unpack themselves into other items (e.g., a chest).

The caller of this API passes in the requested item and an array of existing items and quantities to exchange for it. The API currently takes an array of items to generate but at this time the size of that array must be 1 and the quantity of the new item must be 1.

Any items that can be granted MUST have an exchange attribute in their itemdef. The exchange attribute specifies a set of recipes that are valid exchanges for this item. Exchange recipes are evaluated atomically by the Inventory Service; if the supplied components do not match the recipe, or do not contain sufficient quantity, the exchange will fail.

For Example:

```json
exchange: 101x1,102x1;103x5;104x3,105x3
```

Will allow the item to be exchanged for either one #101 and one #102, five #103s or three #104s and three #105s. See the [Steam Inventory Schema](https://partner.steamgames.com/doc/features/inventory/schema) documentation for more details.

## Options

Heathen provides two options when working with this endpoint.

### Simple

Our Simple variant will save you a lot of effort by handling the result-ready event for you, processing any requested properties and handing you a completed collection of item details when it's all done.

With the simple method, you should provide the item you wish to add as well as any properties you would like us to read from the resulting item. In most cases you won't need additional properties read however if your items have generators on them that create custom properties on creation then you may want to have us read those for you

#### Item Def (input)

The item to grant to the user in exchange for those defined in the Recipe

#### Recipe (input)

An array of [Item Count](../types/item-count.md), expresses the item instances and the quantity from each instance to be used in the exchange.

#### Read Properties (input)

The array of strings representing the keys for each property to be read from the results.&#x20;

#### Callback (input)

The callback is an event that will contain the [UEResult](../enumerators/ueresult.md) of the request and an array of [Item Detail With Properties](../types/item-detail-with-properties.md)

#### Return Value

Always true when called by a regular user, and always false when called by a Steam Game Server.

### Example

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Note that we never return the result handle to you, we track this handle, process the items, read the requested properties and destroy the handle for you returning to you the resulting data in an array.

### Native

The native Steam API works by issuing the request and returning an Item Request Handle when the request is filled Steam will execute the Result Ready callback. You must then read the details, properties and other aspects you desire from the result and then destroy the result handle.

#### Buffer (input)

The buffer to deserialize

### Example

To get the handle you make your request, and check if the request was successful, if so store that request ... you'll need the handle from it later. This will prompt Steam to execute the Result Ready event when the results have been read.

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

When the Result Ready is executed you will need to check if it matches your result handle, fetch the items contained in that result, and for each item fetch whatever additional properties you may need.

<figure><img src="../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Importantly when you are done reading the data returned by that result you need to destroy the handle.

<figure><img src="../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
