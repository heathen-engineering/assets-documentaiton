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

# 🔵 Request Eligible Promo Item Definitions IDs

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Request the list of "eligible" promo items that can be manually granted to the given user.

These are promo items of type "manual" that won't be granted automatically. An example usage of this is an item that becomes available every week.

### Callback

A custom event that provides the following details

* Result\
  A UEResult value indicates status
* Eligible Promo Item Defs\
  An array of Item Def IDs (Int32)
* Cached Data\
  True if the data was read from the cache as opposed to fresh from the backend.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>
