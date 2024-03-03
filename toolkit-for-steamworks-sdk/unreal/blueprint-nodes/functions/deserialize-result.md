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

# 🔵 Deserialize Result

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Deserializes a result set and verifies the signature bytes.\
\
This call has a potential soft-failure mode where the handle status is set to Result Expired. [Get Result Items](get-result-items.md) will still succeed in this mode. The "expired" result could indicate that the data may be out of date - not just due to timed expiration (one hour), but also because one of the items in the result set may have been traded or consumed since the result set was generated. You could simply ignore the "expired" result code and continue as normal, or you could request the player with expired data to send an updated result set.

{% hint style="info" %}
You should call [Check Result Steam ID](check-result-steam-id.md) on the result handle when it completes to verify that a remote player is not pretending to have a different user's inventory.\
\
We do this for you if you use the Simple option as described below.
{% endhint %}

## Options

Heathen provides two options when working with this endpoint.

### Simple

Our Simple variant will save you a lot of effort by handling the result-ready event for you, processing any requested properties and handing you a completed collection of item details when it's all done.

With the simple method, you should provide the item you wish to add as well as any properties you would like us to read from the resulting item. In most cases you won't need additional properties read however if your items have generators on them that create custom properties on creation then you may want to have us read those for you

#### User Id (input)

The user who sent the ticket, we will use this to not only validate the inventory data but also that it came from the user that sent it

#### Buffer (input)

The buffer to deserialize

#### Read Properties (input)

The array of strings representing the keys for each property to be read from the results.&#x20;

#### Callback (input)

The callback is an event that will contain the [UEResult](../enumerators/ueresult.md) of the request and an array of [Item Detail With Properties](../types/item-detail-with-properties.md)

#### Return Value

Always true when called by a regular user, and always false when called by a Steam Game Server.

### Example

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Note that we never return the result handle to you, we track this handle, process the items, read the requested properties and destroy the handle for you returning to you the resulting data in an array.

### Native

The native Steam API works by issuing the request and returning an Item Request Handle when the request is filled Steam will execute the Result Ready callback. You must then read the details, properties and other aspects you desire from the result and then destroy the result handle.

#### Buffer (input)

The buffer to deserialize

### Example

To get the handle you make your request, and check if the request was successful, if so store that request ... you'll need the handle from it later. This will prompt Steam to execute the Result Ready event when the results have been read.

<figure><img src="../../../../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure>

When the Result Ready is executed you will need to check if it matches your result handle, fetch the items contained in that result, and for each item fetch whatever additional properties you may need.

<figure><img src="../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Importantly when you are done reading the data returned by that result you need to destroy the handle.

<figure><img src="../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
