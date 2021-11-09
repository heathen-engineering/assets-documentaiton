# 5 Lobbies

## Introduction&#x20;

This scene demonstrates the use of Steam Lobbies and Lobby Manage component.

![](<../../../../.gitbook/assets/image (175).png>)

### What do I learn?

1. Using [Lobby Manager](../../components/lobby-manager.md) to create, browse and join lobbies
2. Using [Lobby Chat Director](../../components/lobby-chat-director.md) to send and receive chat
3. Using Steamworks Inspector to debug lobby&#x20;
4. How to access the Knowledge Base (where you are now)
5. How to acces the support [Discord ](https://discord.gg/6X3xrRc)
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

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initalization of the Steam API on start up.

The manage also has a [Lobby Manager](../../components/lobby-manager.md) component attached which handles the create, search and join of a lobby.

The manage also has a[ Lobby Chat Director](../../components/lobby-chat-director.md) component attached which handles the send and receive of chat through the connected lobby if any

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as depricated. They simply drive the buttons in the menu nothing more.

The only feature of relivence in the demo scripts is a Join method which reads the text in the InputField and hands it off to the [Lobby Manager](../../components/lobby-manager.md) which will attempt to parse the text to a valid Lobby ID and join the lobby if possible.

It is not a typical use case to type in a lobby ID but is used here to enable developers to test mutliple members joining the same lobby.
