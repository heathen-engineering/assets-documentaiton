---
description: Boop on demand!
---

# Play On Demand

## Introduction

{% hint style="info" %}
Part of the [Interaction Tools](../learning/core-concepts/interaction-tools.md) of the UX Complete asset
{% endhint %}

A simple component that helps you hook any UnityAction, UnityEvent or other inspector feature up to a Play One Shot method.

The intent is that you use this tool to configure the source and clip to be played and then use standard Unity features or similar tools such as the Click event on a button or Bolt's ability to call methods to call the PlayOneShot method.

## Definition

### Fields and Attributes

| Type        | Name        | Notes                                 |
| ----------- | ----------- | ------------------------------------- |
| AudioSource | output      | used to play the sound                |
| AudioClip   | sound       | the sound to be played                |
| float       | volumeScale | the scale of the volume for this play |

### Funcitons

```csharp
public void PlayOneShot();
```

Plays the sound configured on the source configured at the volume scale configured.
