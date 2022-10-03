---
description: Documentation for the Lobbies sample scene in the Steamworks Complete asset
---

# 5 Lobbies

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

{% hint style="warning" %}
This sample scene is a Work In Progress (WIP) and is currently only available to [GitHub Sponsors](../../../../company/become-a-sponsor.md). For Unity Asset Store users the [Legacy 5 Lobbies](legacy-5-lobbies.md) article describes the current scene available to you.\
\
Unity Asset Store will be updated with the new scenes at a later date.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

The 5 Lobbies scene demonstrates a few typical uses of lobbies. In the upper left corner of the screen you will see a "Party UI" where we are using a Lobby Manager, Lobby Chat Director and Set User Avatar tools to drive a fully functional party tool. When the user presses play we perform a Quick Match using another Lobby Manager and along with another Lobby Chat Director we simulate a "Session" or "Matchmaking" lobby complete with chat. When the owner of the session lobby presses the Start Session button we simulate starting up the network session and notifying all members of the lobby.

## Party UI

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

At the top left of the screen is our Party UI. The local user's avatar is always shown in the left most slot with party members listed in the 3 smaller slots. Clicking on an empty slot (represented with a + icon) the Invite tool will display

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

From the invite tool you can select an online friend to invite from a drop down list

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Or you can type in your friends "code" to invite them manually ... note your code is displayed under your name ... you can select and copy and paste this into whatever social chat you like.

<figure><img src="../../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

The party system also demonstrates the built in "ready check" feature of Heathen's Lobby tool. A player can click the Set Ready button to mark them selves as ready or the Set Wait to mark them selves as not ready. The UI will update the thumbs up icon or a grey clock to indicate which users are or are not ready.

Below the user icons is the chat window...

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Our using the Lobby Chat Director we have implemented a simple chat system that displays the chatting user's name and icon but in a compact way.

## Session UI

After the party leader ... or if your not in a party a solo player clicks the "Play" button we perform a Quick Match search via the Lobby Manager tool.

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

If the player is the party leader of a party lobby we go ahead and notify the other members of the party of the new lobby to be joined. We now have a "Session" lobby ... that is a public lobby meant for matchmaking. The party can wait here for other players to join or can go ahead and start the session. Similar to the party UI we have a simple chat system at the bottom edge.

The "owner" of the session lobby has a Start Session button in the middle of the UI. Pressing this will simulate the session starting up and will then notify all members of the resulting connection information.

## Scripts

Here we will discus the sample scripts.

{% hint style="danger" %}
Sample / Example scripts are NEVER fit for production use.\
\
They are written in a verbose manner to help you understand what each is doing and to fully demonstrate each aspect they cover. \
\
As a result they are not written with efficiency, stability, maintainability or flexibility in mind. They are written to be read much like an article, so open them up and start reading to under stand how you might create your own UI controllers.
{% endhint %}

### Game UI Controller

{% hint style="info" %}
Read the GameUIController.cs script located in the same folder as the scene. It was written to be highly verbose and heavily commented and will guide you through each function and its use.
{% endhint %}

The Game UI Controller is attached to the Manager GameObject. This controller handles responding to lobby invite requests and joining the user to the correct lobby.&#x20;

#### OnLobbyInviteArgumentDetected

This is a method within the controller and responds to the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component's Lobby Invite Argument Detected event. This event is raised when Heathen's Steamworks detects that the game was launched with a lobby ID in its command line arguments. This would happen if the user had accepted an invite to a lobby before launching the game.

This function will request data about this lobby, when received will join it either as a party lobby request or session lobby request depending on the lobby type.

#### OnLobbyJoinRequested

This is a method within the controller and responds to the [Overlay Manager](../../components/overlay-manager.md) component's Lobby Join Requested event. This would be raised if the user accepted a lobby invite while already in the game.

This function will request data about this lobby, when received will join it either as a party lobby request or session lobby request depending on the lobby type.&#x20;

#### DevBoxJoinLobby

This is a method within the controller and responds to the Join button from the Dev Box located at the lower centre of the screen. This is useful when performing dev testing in Unity Editor ... note Unity Editor doesn't play nicely with Steam Overlay so a traditional "invite" may not pop the Steam Overlay dialogs you need to accept in order for the invite system to work as expected.&#x20;

Thus the Dev Box is a work around for use by developers working in the Unity Editor. This function simply simulates having received a lobby ID via an invite and performs the same steps as if it had.

### Party UI Controller

{% hint style="info" %}
Read the PartyUIController.cs script located in the same folder as the scene. It was written to be highly verbose and heavily commented and will guide you through each function and its use.
{% endhint %}

The Party UI Controller is attached to the Canvas/Party Lobby GameObject. This controller handles the party UI and works with [Lobby Manager](../../components/lobby-manager.md) and [Lobby Chat Director](../../components/lobby-chat-director.md) to deliver a full featured party system.&#x20;

Our example party system handles up to 4 players in a party. It indicates which of the members is the party "leader" via a gold star and indicates the ready state of each party member via a green or grey icon.&#x20;

The party system features a simple "Invite" UI which can be opened by click any empty slot. The Invite UI displays the local player's "code" ... which is simply the [Account ID](../../quick-start-guide/csteamid.md#account-id) portion of the player's [CSteamID](../../quick-start-guide/csteamid.md). The player can either share this code out and type a friends code into the text box to invite them.&#x20;

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

We have also provided a simple "Friends List" in the drop down button to the right which when expanded will show a list of all the friends that are currently online and when one is selected it will pre-populate the Friend ID field for you.

The functions of the Party UI Controller are largely event handlers being triggered by events from the [Lobby Manager](../../components/lobby-manager.md) and [Lobby Chat Director](../../components/lobby-chat-director.md) located on the same GameObject

### Session UI Controller

{% hint style="info" %}
Read the SessionUIController.cs script located in the same folder as the scene. It was written to be highly verbose and heavily commented and will guide you through each function and its use.
{% endhint %}

The Session UI Controller script is very similar to the PartyUIController but demonstrates a more complex use of the lobby chat system and Lobby metadata. At the top of the script you will see we define the ChatMessage and SessionSettings structures.&#x20;

#### ChatMessage

ChatMessage is a simple serializable struct and is used along with the Lobby Chat Director to send more complex data over the Lobby Chat system than simple text messages. Using this structure we are able to send authentication ticket data via the chat system along with of course simple text messages.

The most interesting use of this is simply for authentication. When a user joins the lobby they will get and send there [Authentication](../../guides/authentication.md) ticket by creating a new ChatMessage value and storing the ticket data within. The ChatMessage being a serializable type can be handed to the [Lobby Chat Director](../../components/lobby-chat-director.md) which will serialize it and send it over Steam Lobby Chat.

### Party UI Chat Message

The Party UI Chat Message behaviour is a simple behaviour that simply gives us an easy to access reference for the [SetUserAvatar, ](../../components/set-user-avatar.md)[SetUserName ](../../components/set-user-name.md)and text message on our chat message prototype. Despite its name we use this for all chat messages that is for both the Party chat and the Session chat.
