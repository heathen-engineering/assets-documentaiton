---
description: Code free drag and drop party lobby tool
---

# Party Lobby Control

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Create a party lobby and its UI fully featured including in game friend invite with ZERO code required.

![](../../../../.gitbook/assets/image.png)

The Party Lobby Control is a UI behaviour component that manages a lobby representing a player party and the UI elements associated with that. This sort of "Party UI" is common in most team and  coop games such as MOBAs, Team Shooters, party games and more. One of the most typical examples of a party lobby can seen in DOTA2.

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>DOTA 2 home screen captured 2022-10-30</p></figcaption></figure>

The purpose of a "party lobby" also known as a "group lobby" is to gather Friends that wish to play together, most typically in a coop game though you do see Group/Party systems in competitive games as well particularly party games.

Party or Group type lobbies differ from Session type lobbies in that they only group a set of friends together. They do not attempt to matchmake or define the state of a "session".

{% hint style="info" %}
In this case let "session" refer to a session of game play e.g. a match, mission, race, level, etc.
{% endhint %}

Session lobbies in contrast are not typically concerned with friends so much as they are with meaningful matchmaking e.g. placing players of similar skill, near by region and similar game session preferences together in order to facilitate a timely and entertaining "session". The members in a "Party" would typically join the same "Session" lobby when looking to play a game.&#x20;

For example in DOTA 2 up to 5 players can form a group/party, this is a full "team" in DOTA. When the party leader presses the "Play DOTA" button the game performs a quick match looking for a "Session" that can accommodate the party of players. When the session starts the party of players will be placed on the same team.

## Features

### Create

Automatically handles create and exit of a group lobby. You can always fetch the current group lobby from the Lobby struct.

```csharp
if(Lobby.GroupLobby(out Lobby groupLobby)
{
    //We are in a group lobby
    if(groupLobby.MemberCount > 1)
    {
        //We are not alone in the party
    }
}
```

### Display

Display the user's avatar and the number of slots available to the party/group. When a slot is "filled" that user's avatar will be displayed.

### Friend Invite

The provided prefab implements the [Friend Invite Drop Down](friend-invite-dropdown.md) letting the user invite online friends with the click of a button or to type in a friend's "code" to initiate and invite.

### Chat

When a user is in a party with other player's a simple text based chat interface is displayed. The chat system is used by other tools to notify party members when they should join a specific session lobby. Heathen's session lobby controls will handle this automatically or you can do this your self by prefixing the chat message with \`\[SessionId]\` followed by the ulong id of the session lobby to join

## Prefab

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
