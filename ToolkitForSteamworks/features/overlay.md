# Overlay

{% embed url="https://partner.steamgames.com/doc/features/overlay" %}

> The Steam overlay is a piece of the Steam user interface that can be activated over the top of almost any game launched through Steam. It lets the user access the friends list, web browser, chat, and in-game DLC purchasing.

The Steam overlay is not "in" your game; it is literally the Steam client (aka Steam.exe) rendering over the top of your game's main window. Consequently there is nothing to "debug" about Steam Overlay other than you requesting it to open to a particular dialogue correctly and that your game "pauses" when the overlay is open.

## Development Time

{% hint style="warning" %}
Steam Overlay will not work (correctly) in Unreal Editor or Unity Editor or any similar multi-window application.
{% endhint %}

Steam Overlay renders over the active window of whatever application initialised the SteamAPI. When you are developing and debugging "in editor", this will cause Steam to treat your editor as "the game". Unity, Unreal and most development tools have many windows, not one and as a result, the Steam Overlay will not work at all or will work unpredictably.

## Examples

### Is Active

To check if the Steam Overlay is currently open or to react to it opening&#x20;

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add the Overlay component to a GameObject and add the Overlay Activated event

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

### C\#

```csharp
// Register the event On Game Overlay Activated
SteamTools.Events.OnGameOverlayActivated += HandleActivated;

// The handler will take the form
void HandleActrivated(bool IsShowing)
{
    if(IsShowing)
        ;// Pause your game?
    else
        ;// Unpause your game?
}

// Alternativly you can check
if (Overlay.Client.IsShowing)
    ; // Its showing
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
### Blueprint

<figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

## C++

```csharp
Coming Soon
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
Coming Soon
```
{% endtab %}
{% endtabs %}

### Open Dialogue

Used to open the overlay to a given dialog, Steam has a number of common dialogs you can open to&#x20;

* Friends
* Community
* Players
* Settings
* Offical Game Group
* Stats
* Achievements

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add the Overlay component to a GameObject

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

And use the Open Dialog Name function to open the overlay to a specific dialogue

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Typical dialog options include

* friends
* community
* players
* settings
* officialgamegroup
* stats
* achievements

## C\#

```csharp
// dialog is an enum of valid options.
Overlay.Client.Activate(dialog);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

## C++

Valid options include

* friends
* community
* players
* settings
* officialgamegroup
* stats
* achievements

```cpp
SteamFriends()->ActivateGameOverlay("friends");
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
SteamFriends.ActivateGameOverlay("friends");
```
{% endtab %}
{% endtabs %}

### Open Invite

Can be used to invite a friend to a Game Session or a Lobby.

{% hint style="info" %}
Steam Lobby is not a game server or a game session it is more akin to a chat room or "Discord DM" where you invite friends to for matchmaking or "party/group" purposes.

\
In contrast inviting a friend to a "Game" aka "Game Session" means to invite them to join a Listen Server (aka P2P Host) or Dedicated Server.
{% endhint %}

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add the Overlay component to a GameObject

<figure><img src="../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

To open the Lobby Invite dialog in the Overlay so the player can choose a friend to invite call Open Lobby Invite

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

To open the Game Invite dialog in the Overlay so the player can choose a friend to invite call Open Connect String Invite

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

## C\#

Use the Activate Invite Dialog function, you can pass in a&#x20;

* String\
  This will be the connection string to a "Game" aka "Game Session" to join. For example if you wanted to invite the player to join you assuming you are a Listen Server you can pass in `UserData.Me.id.ToString()`
* LobbyData\
  This will be the lobby you want to invite the user to, note LobbyData is implicitly convertible to and from ulong, uint and CSteamID so you can use a variable of any of those types as long as its a legitimate Steam Lobby.

```csharp
Overlay.Client.ActivateInviteDialog(target);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

We provide you with 2 nodes as shown below to invite to a connection string (for a game) or an id (for a lobby).

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// for an FString ConnectionString
SteamFriends()->ActivateGameOverlayInviteDialogConnectString(StringCast<ANSICHAR>(*ConnectionString).Get());

// for a CSteamID LobbyId
SteamFriends()->ActivateGameOverlayInviteDialog(LobbyId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// for a string connectionString
SteamFriends.ActivateGameOverlayInviteDialogConnectString(connectionString);

// for a CSteamID lobbyId
SteamFriends.ActivateGameOverlayInviteDialog(lobbyId);
```
{% endtab %}
{% endtabs %}

### Open Remote Play Together

Steam [Remote Play](remote-play.md) feature allows a player to "Stream" the 2nd player to the game. That is the game will operate as if both players are local (couch coop).&#x20;

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add the Overlay component to a GameObject

<figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

Use the Open Remote Play Invite function providing it with the lobby you want to invite through.

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
Overlay.Client.ActivateRemotePlayInviteDialog(lobby);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// for a CSteamID LobbyId
SteamFriends()->ActivateGameOverlayRemotePlayTogetherInviteDialog(LobbyId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// for a CSteamID lobbyId
SteamFriends.ActivateGameOverlayRemotePlayTogetherInviteDialog(lobbyId);
```
{% endtab %}
{% endtabs %}

### Open Store

You can open the Steam Overlay to the store of any given App ID. This is useful for directing players to your game from a demo, to DLC or to companion apps.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add the Overlay component to a GameObject

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

You can then use the&#x20;

* Open Store
* Open Store Add to Cart
* Open Store Add to Cart and Show

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

## C\#

Flag indicates

* None
* Add to Cart
* Add to Cart and Show

```csharp
Overlay.Client.Activate(appID, flag);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// For AppId_t AppId 
// and 
// EOverlayToStoreFlag Flag
SteamFriends()->ActivateGameOverlayToStore(AppId, Flag);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// For AppId_t appID
// and 
// EOverlayToStoreFlag flag
SteamFriends.ActivateGameOverlayToStore(appID, flag);
```
{% endtab %}
{% endtabs %}

### Open User Dialog

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Add the Overlay component to a GameObject

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Each dialog has its own function as shown below, each takes a [User](user.md) component to indicate the user you want to open it for.

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
// dialog is a string
// - steamid                :User Profile
// - chat                   :User Chat
// - jointrade              :Inventory trade dialog
// - stats                  :User Stats
// - achievements           :User Achievements
// - friendadd              :Add Friend dialog
// - friendremove           :Remove Friend dialog
// - friendrequestaccept    :Accept friend request
// - friendrequestignore    :Ignore friend reqeust
API.Overlay.Client.Activate(dialog, steamId);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

## &#x20;C++

```cpp
// dialog is a string
// - steamid                :User Profile
// - chat                   :User Chat
// - jointrade              :Inventory trade dialog
// - stats                  :User Stats
// - achievements           :User Achievements
// - friendadd              :Add Friend dialog
// - friendremove           :Remove Friend dialog
// - friendrequestaccept    :Accept friend request
// - friendrequestignore    :Ignore friend reqeust
SteamFriends()->ActivateGameOverlayToUser("steamid", UserId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// dialog is a string
// - steamid                :User Profile
// - chat                   :User Chat
// - jointrade              :Inventory trade dialog
// - stats                  :User Stats
// - achievements           :User Achievements
// - friendadd              :Add Friend dialog
// - friendremove           :Remove Friend dialog
// - friendrequestaccept    :Accept friend request
// - friendrequestignore    :Ignore friend reqeust
SteamFriends.ActivateGameOverlayToUser(dialog, steamId);
```
{% endtab %}
{% endtabs %}

### Open Web

{% tabs %}
{% tab title="Toolkit for Unity " %}
## Code Free

Add the Overlay component to a GameObject

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

You can use the Open Web Page function to open the overlay to a specific web page

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
Overlay.Client.ActivateWebPage(url);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// For FString url
SteamFriends()->ActivateGameOverlayToWebPage(StringCast<ANSICHAR>(*url).Get());
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
SteamFriends.ActivateGameOverlayToWebPage(url);
```
{% endtab %}
{% endtabs %}
