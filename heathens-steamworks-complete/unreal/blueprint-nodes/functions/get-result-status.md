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

# 🔵 Get Result Status

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Get the items associated with an inventory result handle.

### Result Handle

The Inventory Result Handle to read data from

### Return Value

The UEResult status represents the status of the request.

* Pending\
  Still in progress.
* OK\
  Done, the request has been completed successfully and the result is ready.
* Expired\
  Done, result ready, maybe out of date.
* Invalid Param\
  Error, invalid API call parameters.
* Service Unavailable\
  Error, service is temporarily down, you may retry later.
* Limit Exceeded\
  Error, Operation would exceed per-user inventory limits.
* Fail\
  Error, Generic error.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (227).png" alt=""><figcaption></figcaption></figure>
