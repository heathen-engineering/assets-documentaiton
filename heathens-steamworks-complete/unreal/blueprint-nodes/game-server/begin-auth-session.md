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

# 🔵 Server Begin Auth Session

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

Authenticate the ticket from the entity Steam ID to be sure it is valid and isn't reused.

### Auth Ticket

The auth ticket to validate.

### Steam ID

The entity's Steam ID that sent this ticket.

### Return Value

The [UEBeginAuthSessionResult](../enumerators/uebeginauthsessionresult.md) indicates the state of the request.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (268).png" alt=""><figcaption></figcaption></figure>
