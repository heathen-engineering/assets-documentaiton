---
description: 👉Boop!
---

# Play On Click

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

A simple componenet which plays an audio clip when a click is detected. This uses Unity's IPointerClickHandler to detect when a click occurs and what buttons where involved with it if any.

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

