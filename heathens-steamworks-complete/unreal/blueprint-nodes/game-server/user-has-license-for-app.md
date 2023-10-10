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

# 🔵 User Has License for App

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
Only valid for Steam Game Servers
{% endhint %}

Check if the user owns a specific piece of [Downloadable Content (DLC)](https://partner.steamgames.com/doc/store/application/dlc).\
\
This can only be called after sending the user auth ticket to [Begin Auth Session](begin-auth-session.md)

### User

The Steam ID of the user that sent the auth ticket.

### App

The DLC App ID to check if the user owns it.

### Return Value

The [UEUserHasLicenseForAppResult](../enumerators/ueuserhaslicenseforappresult.md) value

## Nodes

<figure><img src="../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>
