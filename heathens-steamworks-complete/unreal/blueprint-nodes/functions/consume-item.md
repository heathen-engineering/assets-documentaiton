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

# 🔵 Consume Item

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Consumes items from a user's inventory. If the quantity of the given item goes to zero, it is permanently removed.

Once an item is removed it cannot be recovered. This is not for the faint of heart - if your game implements item removal at all, a high-friction UI confirmation process is highly recommended.

## Options

Heathen provides two options when working with this endpoint.

### Simple

Our Simple variant will save you a lot of effort by handling the result-ready event for you, processing any requested properties and handing you a completed collection of item details when it's all done.

With the simple method, you should provide the item you wish to add as well as any properties you would like us to read from the resulting item. In most cases you won't need additional properties read however if your items have generators on them that create custom properties on creation then you may want to have us read those for you

#### Item Instance Id (input)

The specific item instance to be consumed

#### Quantity (input)

The number of items to be consumed from the instance

{% hint style="info" %}
Think of an "Item Instance" as a stack of that item for example a stack of gold. An instance may contain 0 or many of that particular item type&#x20;
{% endhint %}

#### Read Properties (input)

The array of strings representing the keys for each property to be read from the results. This isn't likely to be used for Consume but is technically possible so is exposed here for you.

#### Callback (input)

The callback is an event that will contain the [UEResult](../enumerators/ueresult.md) of the request and an array of [Item Detail With Properties](../types/item-detail-with-properties.md)

#### Return Value

Always true when called by a regular user, always false when called by a Steam Game Server.

### Example

<figure><img src="../../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

Note that we never return the result handle to you, we track this handle, process the items, read the requested properties and destroy the handle for you returning to you the resulting data in an array.

### Native

The native Steam API works by issuing the request and returning an Item Request Handle when the request is filled Steam will execute the Result Ready callback. You must then read the details, properties and other aspects you desire from the result and then destroy the result handle.

#### Item Instance Id (input)

The specific item instance to be consumed

#### Quantity (input)

The number of items to be consumed from the instance

{% hint style="info" %}
Think of an "Item Instance" as a stack of that item for example a stack of gold. An instance may contain 0 or many of that particular item type&#x20;
{% endhint %}

### Example

To get the handle you make your request, and check if the request was successful, if so store that request ... you'll need the handle from it later. This will prompt Steam to execute the Result Ready event when the results have been read.

<figure><img src="../../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

When the Result Ready is executed you will need to check if it matches your result handle, fetch the items contained in that result, and for each item fetch whatever additional properties you may need.

<figure><img src="../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Importantly when you are done reading the data returned by that result you need to destroy the handle.

<figure><img src="../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
