---
description: 🚪Boop!
---

# Play On Enter

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../features/interaction-tools.md) of the UX Complete asset
{% endhint %}

A simple component that plays the configured sound when the pointer enters. This uses Unity's IPointerEnterHandle.

## Definition

### Fields and Attributes

| Type        | Name        | Notes                                 |
| ----------- | ----------- | ------------------------------------- |
| AudioSource | output      | used to play the sound                |
| AudioClip   | sound       | the sound to be played                |
| float       | volumeScale | the scale of the volume for this play |

