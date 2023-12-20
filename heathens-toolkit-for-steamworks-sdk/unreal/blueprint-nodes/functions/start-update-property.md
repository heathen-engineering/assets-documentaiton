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

# 🔵 Start Update Property

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Starts a transaction request to update [dynamic properties](https://partner.steamgames.com/doc/features/inventory/dynamicproperties) on items for the current user. This call is rate-limited by the user, so property modifications should be batched as much as possible (e.g. at the end of a map or game session). After calling [Set Property](set-property.md) or [Remove Property](remove-property.md) for all the items that you want to modify, you will need to call [Submit Update Properties](submit-update-property.md) to send the request to the Steam servers. A [Steam Inventory Result Ready](../events/inventory-results-ready.md) callback will be fired with the results of the operation.

### Return Value

Returns an Update Handle that can be used with Set Property, Remove Property and Submit Update Properties.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure>
