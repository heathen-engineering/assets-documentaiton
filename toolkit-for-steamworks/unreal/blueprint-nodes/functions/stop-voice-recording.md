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

# 🔵 Stop Voice Recording

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Stops voice recording.\
\
Because people often release push-to-talk keys early, the system will keep recording for a little bit after this function is called. As such, [Get Voice](get-voice.md) should continue to be called until it returns [Not Recording](../enumerators/uevoiceresult.md), only then will voice recording be stopped.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>
