# Cursor Animation

## Introduction

{% hint style="info" %}
Part of the [Cursor System](../learning/core-concepts/cursor-tools.md) of the UX Foundation and UX Compelete assets
{% endhint %}

Defines the animation conditions for a cursor state

## Definition

### Fields and Attributes

| Type         | Name            | Notes                                                |
| ------------ | --------------- | ---------------------------------------------------- |
| bool         | loop            | should this aniamtion loop                           |
| Texture2D\[] | textureArray    | lists the frames of the animation                    |
| float        | framesPerSecond | the number of frames that shold be cycled per second |

