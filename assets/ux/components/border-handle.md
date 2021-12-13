---
description: Get a handle on window size
---

# Border Handle

## Introduction

{% hint style="info" %}
Part of the [Window System](../learning/core-concepts/window-tools.md) of the UX Complete asset
{% endhint %}

Meant to be added to a Unity uGUI object or similar element on a Window. This expects to be the child of a window and can be at any depth you like. Its rect is what will respond to pointer input annd manage the resize operations of the parent window.

When the user grabs and drags this componenet's RectTransform a drag delta will be calculated based on the type of handle this is. The resulting delta (difference) will be reported to the parent window and used to change the size of the window.

This does work with both the old and new Input Systems from Unity.

## Definition

### Fields and Attributes

| Type                                  | Name   | Notes                           |
| ------------------------------------- | ------ | ------------------------------- |
| [GrabHandle](../enums/grab-handle.md) | handle | what part of the handle is this |
