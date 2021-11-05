---
description: 👇Boop!
---

# Play On Down

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../features/interaction-tools.md) of the UX Complete asset
{% endhint %}

A simple componenet which plays an audio clip when a mouse down is detected. This uses Unity's IPointerDownHandler to detect when a pointer down occurs and what buttons where involved with it if any.

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

