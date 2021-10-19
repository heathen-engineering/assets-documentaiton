---
description: Getting to know the Heathen selection system
---

# Selection System

{% hint style="info" %}
Selection System is an upcoming feature of the UX V2 asset family and will be available to both the UX Complete and UX Foundation assets.
{% endhint %}

## Introduction

The Selection System tool makes it a simple matter to handle single and multi-select behaviours and to understand what kinds of objects have been selected e.g. selecting enemies, selecting inventory items, etc. The system is not dependent on Unity's UI frameworks and can be used with world objects or any UI objects that can be assoceated with a MonoBehaviour.

Selection System allows you to mark selectable objects and to decorate them with "[tags](../system-core/scriptable-tags.md)". Tags can be used to query the currently selected objects ... for example you can return a list of all of the friendly units currently selected by the player or perhaps you prefer a list of all inventory items currently selected by the player. Tags can also be used to restrict selection ... that is you can cause the system to ignore attempts to select objects that have given tags or that lack given tags making it easy to configure situations such as an RTS with teams where player's shouldn't be able to select opposing player's objects.
