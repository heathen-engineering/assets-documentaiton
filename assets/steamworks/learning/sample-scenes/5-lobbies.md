---
description: Documentation for the Lobbies sample scene in the Steamworks Complete asset
---

# 5 Lobbies

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of Steam Lobbies and Lobby Manage component.

![](<../../../../.gitbook/assets/image (183) (1) (1) (1).png>)

### What do I learn?

1. Using [Lobby Manager](../../components/lobby-manager.md) to create, browse and join lobbies
2. Using [Lobby Chat Director](../../components/lobby-chat-director.md) to send and receive chat
3. Using Steamworks Inspector to debug lobby&#x20;
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

### Instructions

#### To create a lobby

1. Make sure you have Steam Client started and logged into a valid Steam user
2. Run the simulation
3. Click the Create Lobby button
4.  Observe the console log which will report

    "New lobby created"
5. Open the Steamworks Inspector as instructed in the scene and observe that you have a lobby and it contains the expected information such as you being listed as the owner

#### To join a lobby

1. On another machine which we will call "HOST" and with a different Steam User follow the steps for "Create a Lobby"
2. On HOST observe the ID of the lobby via the Steamworks Inspector and make note of it
3.  On a different machine and with a different user than was used on HOST to create the lobby

    Type the ID into the input field provided
4. Click the Join Lobby button
5. Using Steamworks Inspector obs

#### To browse lobbies

1. Make sure you have a Steam Client started and logged into a valid Steam user
2. Run the simulation
3. Click the Browse Lobbies button
4. Observe the console log which will report the lobbies found
5. Observer the Example Browser UI elements which will populate with the lobbies found

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

The manage also has a [Lobby Manager](../../components/lobby-manager.md) component attached which handles the create, search and join of a lobby.

The manage also has a[ Lobby Chat Director](../../components/lobby-chat-director.md) component attached which handles the send and receive of chat through the connected lobby if any

### Example Browser

The Example Browser game object located under the Canvas game object demonstrates a very crude example of a lobby browser. The primary intent here is **NOT** to give you a production ready UI component for browsing lobbies but to show you how simple it is to make your own.

The Example Browser has a component on it ExamplePopulateResultList this component's source code is in the scene sample code. It simply handles the [evtFound ](../../components/lobby-manager.md#evtfound)event from the [Lobby Manager](../../components/lobby-manager.md) and uses the provided array of [Lobby ](../../objects/lobby.md)objects to populate the UI.

The UI is populated by simply instantiating a templated UI object which implements the example script LobbyDisplayRecord. LobbyDisplayRecord does nothing more than assign the input Lobby's name to a label and on click of a button tries to join the lobby.

In a production ready lobby system you would use a more elaborate display record that showed the user information relevant to your game such as game mode, party size or whatever other information might be relevant. You would also want to handle the join request to know if it was successful ... its possible the join was rejected. Our example scripts have events for Join and Join Error as a demonstration of how you might detect when this occurs.

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as deprecated. They simply drive the buttons in the menu nothing more.

The demo script has a Join method which reads the text in the InputField and hands it off to the [Lobby Manager](../../components/lobby-manager.md) which will attempt to parse the text to a valid Lobby ID and join the lobby if possible.

It is not a typical use case to type in a lobby ID but is used here to enable developers to test multiple members joining the same lobby.

## Lobby Browser

![Screen shot of the Example Populate Result List component on the Example Browser Game Object](<../../../../.gitbook/assets/image (153) (1) (1).png>)

![Screen shot of the Lobby Display Record template referenced by the Example Browser](<../../../../.gitbook/assets/image (178) (1) (1) (1).png>)

