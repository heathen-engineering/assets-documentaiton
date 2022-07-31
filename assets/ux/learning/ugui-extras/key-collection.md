---
description: >-
  Documentation for the asset formerly known as On Screen Keyboard. Create
  virtual keyboards, in world pin pads, alien computer consoles and so much
  more.
---

# Key Collection

## Introduction

### What

Simply\
Lets you create keyboards, pin pads, alien computer consoles or really any collection of "keys" as a simple Unity UI object.\
\
Specifically\
Key Collection is a controller that manages multiple "keys"  and works in concert with related tools such as the Output Manger to direct the results of key strokes to desired targets.

{% hint style="info" %}
Key Collection can handle any string output that Unity understands, that means it can handle all the language, character sets, etc. that Unity can handle.

When coupled with the [Ligature tool](ligature-tools.md) it can handle complex multi-key ligatures as used by many languages including but not limited to Korean, Japanese, west accent marks, etc.
{% endhint %}

### Why

Traditionally our tool has been used in games where you cant or don't want the user to use a traditional keyboard. For example touch screen devices such as phones, tables, etc. Consoles or similar. It lets you render a keyboard of your specification to the screen and handles the key presses to populate string fields, input fields or similar.

{% hint style="warning" %}
Key Collection is not a "HID" (human interface device) that is the computer will not see it as a keyboard, it will not trigger the Intput.GetKey(XXX) to be true, etc. It is simply a collection of UnityEngine.UI.Buttons being controlled and managed to simulate any sort of key collection including of course an on screen keyboard.
{% endhint %}

This can also be used for world canvas UIs; for example you create a pin pad on a security door in your game and have it actually respond to mouse clicks from the user. There is no reason to restrict it to human language either, you can create a completely alien console, keyboard, etc. and make it actually work in the 3D world or as part of your traditional 2D UI.

### How

Key Collection is a simple Unity component that can be added to a GameObject. You can add additional tools and features such as KeyCollectionOutputManager and Designer to manage the output from the collection e.g. direct key strokes to an input field for example, or to help you design your keyboard such as to generate a standard QWERTY or similar board.

## Configuration

### Key Collection

![](<../../../../.gitbook/assets/image (102).png>)

The root of the system Key Collection is the behavior that manages all others. This component contains your high level configuration options and exposes collection level events to the inspector

#### Use Shift Toggle

Should the shift key act like a toggle e.g. press to turn on and again to turn off or should the shift function require the user to hold it to use it

#### Alt Gr Toggle

Should the Alt Gr key act like a toggle e.g. press to turn on and again to turn off or should the Alt Gr function require the user to hold it to use it

#### User Key Hold

When a user presses and holds a key down should the input repeat

#### Repeat Time

If Use Key Hold is true how frequently should the key repeat while held

#### Keyboard Game Event

A reference to a [Game Event](../../../system-core/game-events.md) to be invoked when the user presses a key

#### Keyboard Key Pressed

A standard Unity event that is invoked when the user presses a key

### Key Collection Output Manager

![](<../../../../.gitbook/assets/image (103) (1).png>)

This component directs the results of key presses according to its configuration. The most common configuration is shown above. When configured for Event System the output manager will monitor the Unity Event system and remember the most recently selected UnityEngine.UI.InputField or TMPro.TextMeshProInputField. When a key is pressed the output will be directed to that most recently focused input field.

#### Input Field

![](<../../../../.gitbook/assets/image (104).png>)

When configured for Input Field the designer can specify a UnityEngine.UI.InputField. In this mode the output will always be directed to this specific InputField

#### Text

![](<../../../../.gitbook/assets/image (105).png>)

When configured for Text the designer can specify a target UnityEngine.UI.Text. in this mode the output will always be directed to this specific text field

#### Component

![](<../../../../.gitbook/assets/image (106).png>)

When configured for Component, the designer can select a GameObject and then select any component behavior on that GameObject. The designer can then indicate any string field or attribute on that component behavior to be the target of the output.

#### Function

![](<../../../../.gitbook/assets/image (107).png>)

When configured for Function the designer can specify a target function via a Unity Event. The output will be directed to that function as an input parameter of type KeyCollectionKey. It is up to that function handle the input from there.

### Key Collection Designer

![](<../../../../.gitbook/assets/image (108).png>)

The Key Collection Designer assists the user in creating a new keyboard from scratch. You can quickly generate common boards such as QWERTY, AZERTY, etc. and then modify the collection from there manually.

{% hint style="info" %}
Remember the collection is just a GameObject and each key within it is again just a regular GameObject. You can simply add or remove them from the scene as you see fit and change there settings as you require
{% endhint %}

### Key Collection Template Manager

![](<../../../../.gitbook/assets/image (109) (1).png>)

The Key Collection Template Manager allows you to save your configuration as an asset object for easy import into other scenes or projects. With modern versions of Unity, a nested Prefab can do much the same however this tool can be useful for quickly swapping out key templates (the prefab used to generate the keys).

## Eastern Language Support

A common question is can this tool support easter langauges where ligatures are used. The answer is yes we have a [Ligature Tool](ligature-tools.md) which can enable the Key Collection to deal with these use cases.

