---
description: 👉Boop!
---

# Play On Click

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

A simple component which plays an audio clip when a click is detected. This uses Unity's IPointerClickHandler to detect when a click occurs and what buttons were involved with it if any.

## Definition

### Fields and Attributes

| Type        | Name              | Notes                                                               |
| ----------- | ----------------- | ------------------------------------------------------------------- |
| AudioSource | output            | used to play the sound                                              |
| AudioClip   | sound             | the sound to be played                                              |
| float       | volumeScale       | the scale of the volume for this play                               |
| bool        | alwaysPlay        | Should the sound play on any click event regardless of buttons used |
| bool        | handleLeftClick   | play when left button used                                          |
| bool        | handleRightClick  | play when right button used                                         |
| bool        | handleMiddleClick | play when middle button used                                        |

