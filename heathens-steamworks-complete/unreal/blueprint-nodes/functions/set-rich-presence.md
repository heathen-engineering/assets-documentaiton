---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🔵 Set Rich Presence

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Sets a Rich Presence key/value for the current user that is automatically shared to all friends playing the same game.

Each user can have up to 20 keys set

There are two special keys used for viewing/joining games:

* "status" - A UTF-8 string that will show up in the 'view game info' dialog in the Steam friends list.
* "connect" - A UTF-8 string that contains the command-line for how a friend can connect to a game. This enables the 'join game' button in the 'view game info' dialog, in the steam friends list right click menu, and on the players Steam community profile. Be sure your app implements [ISteamApps::GetLaunchCommandLine](https://partner.steamgames.com/doc/api/ISteamApps#GetLaunchCommandLine) so you can disable the popup warning when launched via a command line.

There are three additional special keys used by the [new Steam Chat](https://steamcommunity.com/updates/chatupdate):

* "steam\_display" - Names a rich presence localization token that will be displayed in the viewing user's selected language in the Steam client UI. See [Rich Presence Localization](https://partner.steamgames.com/doc/api/ISteamFriends#richpresencelocalization) for more info, including a link to a page for testing this rich presence data. If steam\_display is not set to a valid localization tag, then rich presence will not be displayed in the Steam client.
* "steam\_player\_group" - When set, indicates to the Steam client that the player is a member of a particular group. Players in the same group may be organized together in various places in the Steam UI. This string could identify a party, a server, or whatever grouping is relevant for your game. The string itself is not displayed to users.
* "steam\_player\_group\_size" - When set, indicates the total number of players in the steam\_player\_group. The Steam client may use this number to display additional information about a group when all of the members are not part of a user's friends list. (For example, "Bob, Pete, and 4 more".)

### Return Value

**true** if the rich presence was set successfully.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (313).png" alt=""><figcaption></figcaption></figure>
