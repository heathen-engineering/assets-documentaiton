# Steam Input

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

First you should understand what Steam Input is and is not, the only real place to do so is via Valve's documentation and videos on the feature.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/steam_controller" %}

## In-Game Action file

{% embed url="https://partner.steamgames.com/doc/features/steam_controller/iga_file" %}

This is how you define what action sets, layers and actions your game has and how they are used (loosly). Using this Steam's controller binding system can be used to map various controls to your actions and your game can thus be blisfullly unaware of what IO device is actually driving the game.

### [Action Set](../../objects/input-action-set.md)

An action set is simply a container of layers and actions. For example you might have 1 set of actions you use in your menu and another you use in gameplay so you might have an action set `menuActions` and another `gameActions` .

### [Action Set Layer](../../objects/input-action-set-layer.md)

An action set layer is a mask layed over top of an action set. They are defined as a member of the action set and simply modify the set of actions activated by the set. An example might be a layer that adds extra mappings such as a sniper mode when a valid weapon is equiped or vehicle type specific actions such as gas, brea, throttle up/down, etc.

### [Action](../../objects/input-action.md)

An action is ... well the action the player has requested such as jump, walk, shoot, etc. These are defined as members of an action set or action set layer and can specify what kind of action they are e.g. analog or digital and if analog what mode e.g. stick, absolute mouse, etc.

## To Create

Steam Input objects can be created in your [Steam Settings](../../objects/steam-settings.md) object

![](<../../../../.gitbook/assets/image (158) (1).png>)

### Analog vs Digital Actions

You can toggle your Action types by simply clicking the AI/DI button

AI represents an "Analog Input"

DI represents a "Digital Input"
