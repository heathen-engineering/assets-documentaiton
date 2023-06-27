---
description: Documentation for the Lobbies sample scenes in the Steamworks Complete asset
---

# Lobby

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

<figure><img src="../../../../../.gitbook/assets/image (6) (2) (1).png" alt=""><figcaption><p>Session Lobby Screen Shot</p></figcaption></figure>

The Quick Match Example and Session Lobby sample scenes demonstrate the use of our lobby tools, systems and UI elements.

## Quick Match Example

Demonstrating the most common use case for Steam Lobby and how it can be accomplished code free using Heathen's [Party Lobby Control](../../../for-unity-game-engine/ui-components/party-lobby-control.md) and [Quick Match Lobby Control](../../../for-unity-game-engine/ui-components/quick-match-lobby-control.md) components. This code free example uses no custom code at all and handles the use case most common to hobbyist and enthusiast multiplayer game projects.

<figure><img src="../../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The Quick Match Example scene simply cant get any simpler. With only 2 functional UI elements and zero custom code this scene handles forming players in a friend group/party, searching for and selecting or creating a new lobby and reporting when that lobby is full. You can easily connect this scene to any networking HLAPI of your choice and have a functional party + matchmaking multiplayer session assuming you have a network demo scene you can load when your lobby is full.

## Session Lobby

{% hint style="success" %}
Additional information can be found [here](session-lobby.md)!
{% endhint %}

Demonstrates the use of Lobby Manager for a custom session lobby use experience. This scene uses a a single custom script \`SessionLobby\_UIController\` in order to manipulate Heathen's [Lobby Manager](../../ui-components/lobby-manager.md) and UI elements for a bespoke user experience in matchmaking. The purpose of the scene is to get you started with creating your own session lobby user experience.&#x20;

![](<../../../../../.gitbook/assets/image (3) (3).png>)![](<../../../../../.gitbook/assets/image (1) (1) (3).png>)

When you press play in this scene it will search for a matching lobby, if none is found it will create a new lobby matching the Create Arguments in the Lobby Manager. While in a lobby the members are displayed along with simple features like "Ready Check", "Leave" and an indication as to which member is the "owner" of the lobby.

This scene's demo script is marked as "Deprecated" because you are NOT supposed to copy and paste it as is into your game. Rather you are supposed to use it as a learning tool to create your own lobby UI controller suitable for your specific needs. If you are looking for an "out of the box" lobby solution then see our Quick Match Example.
