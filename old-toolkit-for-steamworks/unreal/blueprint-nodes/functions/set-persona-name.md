---
cover: ../../../../.gitbook/assets/Unreal Banner.jpg
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

# 🔵 Set Persona Name

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Sets the current user's persona name, stores it on the server and publishes the changes to all friends who are online. Changes take place locally immediately, and a [Persona State Change ](../events/persona-state-change.md)callback is posted, presuming success. If the name change fails to happen on the server, then an additional [Persona State Change](../events/persona-state-change.md) callback will be posted to change the name back, in addition to the final result available in the callback.&#x20;

### Name

The name to apply

### Callback

An event is executed when the process is completed. This event will include&#x20;

#### Success

**true** if the name change is completed successfully.

#### Local Success

**true** if the name change was retained locally. We might not have been able to communicate with Steam

#### Result

A [UEResult ](../enumerators/ueresult.md)value indicating the result of the operation.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (27) (1) (1).png" alt=""><figcaption></figcaption></figure>
