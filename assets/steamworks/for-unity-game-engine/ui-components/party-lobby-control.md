---
description: Code free drag and drop party lobby tool
---

# Party Lobby Control

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

Create a party [lobby ](../../../../company/steam/steamworks/multiplayer/matchmaking-tools.md)and its UI fully featured including in game friend invite, chat, and more with ZERO code required.

![](<../../../../.gitbook/assets/image (5) (4).png>)

The Party Lobby Control is a UI behaviour component that manages a lobby representing a player party and the UI elements associated with that. This sort of "Party UI" is common in most team and  coop games such as MOBAs, Team Shooters, party games and more. One of the most typical examples of a party lobby can seen in DOTA2.

<figure><img src="../../../../.gitbook/assets/image (4) (3).png" alt=""><figcaption><p>DOTA 2 home screen captured 2022-10-30 by Loden Darkstar</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Halo Infinite multiplayer mode scree captured 2022-10-30 by Loden Darkstar</p></figcaption></figure>

The purpose of a "party lobby" also known as a "group lobby" is to gather Friends that wish to play together, most typically in a coop game though you do see Group/Party systems in competitive games as well particularly party games.

Party or Group type lobbies differ from Session type lobbies in that they only group a set of friends together. They do not attempt to matchmake or define the state of a "session".

{% hint style="info" %}
In this case let "session" refer to a session of game play e.g. a match, mission, race, level, etc.
{% endhint %}

Session lobbies in contrast are not typically concerned with friends so much as they are with meaningful matchmaking e.g. placing players of similar skill, near by region and similar game session preferences together in order to facilitate a timely and entertaining "session". The members in a "Party" would typically join the same "Session" lobby when looking to play a game.&#x20;

For example in DOTA 2 up to 5 players can form a group/party, this is a full "team" in DOTA. When the party leader presses the "Play DOTA" button the game performs a quick match looking for a "Session" that can accommodate the party of players. When the session starts the party of players will be placed on the same team.

## Features

### Create

Automatically handles create and exit of a group lobby. You can always fetch the current group lobby from the [Lobby ](../../data-layer/lobby-data.md)struct.

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

![](<../../../../.gitbook/assets/image (194).png>)

The provided prefab implements the [Friend Invite Drop Down](friend-invite-dropdown.md) letting the user invite online friends with the click of a button or to type in a friend's "code" to initiate and invite.

### Chat

![](<../../../../.gitbook/assets/image (3) (4).png>)

When a user is in a party with other player's a simple text based chat interface is displayed. The chat system is used by other tools to notify party members when they should join a specific session lobby. Heathen's session lobby controls will handle this automatically or you can do this your self by prefixing the chat message with \`\[SessionId]\` followed by the ulong id of the session lobby to join

### Rich Presence

Optionally sets the \`steam\_player\_group\` and \`steam\_player\_group\_size\` fields in Steam's rich presence updating the Friend List group display.

## Prefab

A production ready prefab is available and configured with the features displayed above. You can see an example of this prefab in use in the [Quick Match Example](../../unity/samples/lobby/#quick-match-example) scene.

<figure><img src="../../../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

## Events

### Session Lobby Invite

```csharp
public LobbyDataEvent evtSessionLobbyInvite;
```

This event is invoked when the user is invited to join a session lobby by the owner of the group lobby. For example if you are in a party with user A and user A uses Heathen's Quick Match to create or join a session you will be invited to join that session and this event will be raised.

### Group Lobby Invite

```csharp
public GameLobbyJoinRequestedEvent evtGroupLobbyInvite;
```

This event is invoked when the user is invited and accepts a lobby invite to a group lobby.

## Fields and Attributes

### User Owner Pip

```csharp
public GameObject userOwnerPip;
```

A reference to the GameObject that should be toggled on or off to indicate the local user is the owner of the party/group lobby or not.

### Ready Button

```csharp
public Button readyButton;
```

Optional, if null this feature will be ignored

A reference to the button the user will click to indicate they are ready to play. This is used to update metadata on the lobby and display a "ready" flag on the UI.

### Not Ready Button

```csharp
public Button notReadyButton;
```

Optional, if null this feature will be ignored

A reference to the button the user will click to indicate they are not ready to play. This is used to update metadata on the lobby and clear the display of the "ready" flag on the UI.

### Leave Button

```csharp
public Button leaveButton;
```

A reference to the button the user will click when they want to leave the group/party.

### Auto Join On Invite

```csharp
public bool autoJoinOnInvite;
```

If toggled to true then when a GameLobbyJoinRequest event is detected if the target lobby is of type group the tool will leave any existing group lobby and join this new lobby.

This is not generally recomended as you should be validating the game state and lobby state before blindly joining but can be useful for quick testing.

### Invite Panel

```csharp
public RectTransfrom invitePanel;
```

A reference to the root GameObject representing the "invite panel". This will be toggled on if an empty slot is clicked and toggled off if the control is "clicked off of"

### Invite Dropdown

```csharp
public FriendInviteDropDown inviteDropdown;
```

A reference to the [invite dropdown](friend-invite-dropdown.md) to be used by the control.

### Slots

```csharp
public LobbyMemberSlot[] slots;
```

An array indicating the number of slots this party will support and the configuration of those slots. See the [Lobby Member Slot](lobby-member-slot.md) article for more information.

### Update Rich Presence Group Data

```csharp
public bool updateRichPResenceGroupData;
```

If true then the \`steam\_player\_group\` and \`steam\_player\_group\_size\` rich presence fields will be set based on the current state of this lobby. This is used to group friends in the friends list in the Steam client.&#x20;

### Max Messages

```csharp
public int maxMessages;
```

The number of message entries to keep in the chat history. The system will delete the oldest chat message from the chat log when these number is exceeded.

### Chat Panel

```csharp
public GameObject chatPanel;
```

The root of the chat UI this will be enabled when the lobby as 2 or more members including the local user.

### Input Field

```csharp
public TMP_InputField inputField;
```

A reference to the TextMesh Pro input field to be used as the chat's input field.

### Scroll View

```csharp
public ScrollRect scrollView;
```

A reference to the scroll rect wrapping the chat message root. This is used to force the scroll to the bottom so the newest message received is always visible.

### Message Root

```csharp
public Transform messageRoot;
```

A reference to the transform which will be made the parent of each incoming chat message.

### My Chat Template

```csharp
public GameObject myChatTemplate;
```

A reference to the GameObject or Prefab that should be instantiated for each message received from the local user.

### Their Chat Template

```csharp
public GameObject theirChatTemplate;
```

A reference to the GameObject or Prefab that should be instantiated for each message received from users other than the local user.

### Lobby

```csharp
public Lobby Lobby { get; set; }
```

The lobby (if any) that is being managed by this control

### Has Lobby

```csharp
public bool HasLobby => get;
```

True if this control is currently managing a lobby

### Is Player Owner

```csharp
public bool IsPlayerOwner => get;
```

True if the local player is the owner of this lobby

### All Players Ready

```csharp
public bool AllPlayersReady => get;
```

True if all players in this lobby have indicated they are ready to play

### Is Player Ready

```csharp
public bool IsPlayerReady { get; set; }
```

Indicates rather or not the local player has been set as ready. This can be read or written to, writing to this field will update the LobbyMetadata of the local user for this lobby.
