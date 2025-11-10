# Rich Presence

**Rich Presence** allows your game to display detailed, dynamic status updates on the Steam Friends List. These updates give friends more context about what a player is doing in-game, enhancing social connection and helping others decide how and when to engage.

<figure><img src="../.gitbook/assets/image (178).png" alt=""><figcaption><p>From <a href="https://partner.steamgames.com/doc/features/enhancedrichpresence">https://partner.steamgames.com/doc/features/enhancedrichpresence</a></p></figcaption></figure>

## [Game-Controlled Strings](https://partner.steamgames.com/doc/features/enhancedrichpresence#2)

Your game sets a custom `steam_display` string using `SetRichPresence`. This string appears below the player's name in their Friends List. It must be short enough to fit on one line—long strings will be truncated.

### Choosing the Right Information

What you display depends on your game's structure. Use Rich Presence to highlight the most relevant, friend-visible data:

#### For Multiplayer Games:

* Time remaining or elapsed
* Players still alive
* Game mode or map name
* Score or progress toward an objective
* Open slots on the server
* Current action (e.g. “In Lobby”, “Selecting Loadout”)

#### For Single-Player Games:

* Current level, chapter, or zone
* Player's activity (“Fighting a boss”, “Exploring the swamps”)
* Difficulty or play style

Even solo experiences can prompt social interaction—watching, chatting, or comparing progress.

## [Friend Grouping](https://partner.steamgames.com/doc/features/enhancedrichpresence#3)

Steam can also show **which friends are playing together** using visual groupings in the Friends List. This helps players see if there's room to join or just to spectate a session.

Use:

* `steam_player_group` to identify the group
* `steam_player_group_size` to specify how many are in it

This works best when based on social logic (e.g. party size, not full match size). For example:

* Dota 2: show party members (up to 5)
* CS:GO: show only mutual friends on the same server

## Steam API & Localization

The following is an example of the Rich Presence language tokens used in Valve's documents

```json
"lang"
{
	"Language"	"english"
	"Tokens"
	{
		"#StatusWithoutScore"	"{#Status_%gamestatus%}"
		"#StatusWithScore"	"{#Status_%gamestatus%}: %SCORE%"
		"#Status_AtMainMenu"	"At the main menu"
		"#Status_WaitingForMatch"	"Waiting for match"
		"#Status_Winning"	"Winning"
		"#Status_Losing"	"Losing"
		"#Status_Tied"	"Tied"
	}
}
```

The idea is that during gameplay, you can set values such as `SetRichPresence("score", "42")`and will be used with the status message appropriately. Your task as a developer is to define what variables you need ... such as "score" in Valve's example. And then to set the `steam_display`value to the token that uses those variables.

### Special Tokens

* status\
  String that will show up in the "View Game Info" dialog in the Steam Friends list.
* connect\
  String that contains the command-line for how a friend can connect to a game. This enables the "Join Game" button in the "View Game Info" dialog.
* steam\_display\
  This should be the name of a token defined in your localization tokens that will be displayed. For example, in the above example, a value of #StatusWithScore would parse either the winning or losing message and the score value, assuming, of course, you have set a `score` and `gamestatus` value.
* steam\_player\_group\
  Indicates to the Steam client that the player is a member of a particular group. Players in the same group may be organized together in various places in the Steam UI. This string could identify a party, a server, or whatever grouping is relevant for your game. The string itself is not displayed to users.
* steam\_player\_group\_size\
  Indicates the total number of players in the steam\_player\_group. The Steam client may use this number to display additional information about a group when all of the members are not part of a user's friends list.

## Examples

### Rich Presence

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

### Rich Presence Setter

This can set a key and value on enable and optionally swap between values when the app gains or loses focus.&#x20;

<figure><img src="../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

### Rich Presence Reader

This can have UserData applied to it `reader.Apply(user)` and when that user's rich presence is updated, it will raise the Evt Update, providing you with details.

<figure><img src="../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

## C\#

Use the UserData struct to set a rich presence value

```csharp
// If you are working with other users' data, you will want to listen on changes for them
Friends.Client.EventFriendRichPresenceUpdate.AddListener(HandleRPUpdate);

// Read someone else's value 
UserData User = 123456;
Friends.Client.RequestFriendRichPresence(User);

//Once you get the message it's been updated
string Value = User.GetRichPresenceValue("keyToRead");
```

The HandleRPUpdate would take the form of

```csharp
private void HandleRPUpdate(FriendRichPresenceUpdate Update)
{
    // Update.App what app is this for
    // Update.Friend what user was this for
    // It's up to you to read what you want from them
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}
