# 🧑‍🤝‍🧑 Matchmaking

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Steam provides matchmaking features through the [Lobby ](matchmaking-tools.md)system and [Steam Game Server](game-server-browser/) systems.

## Lobby

It is important to understand that a lobby is not a server browser, it is not designed to list all possible sessions. Using a lobby for matchmaking is the most common approach for Steam Matchmaking options and involves a player searching for a lobby with metadata values that match their query. To understand Lobby Metadata better have a look at the [Lobby](matchmaking-tools.md) article.

### Can I list all lobbies? No

Steam API at most will return 50 lobbies and in most cases that is 49 more lobbies than you need. The lobby query system is designed such that your user describes the match they want and the Steam API will return the ideal match from the available lobbies.

> What if the exact match the player wants isn't available or what if they don't know exactly what they want?

In that case, you have two options

### What is Quick Match

This is the most common approach in modern games. A quick match is where you search for a lobby that matches the desired game well enough and join it, if no ideal match can be found you create a new lobby with the arguments that match the ideal match and continue to look for near matches.

This means that other players looking for the same match will find your new lobby and join you. Typically a modern game will also be looking for near matches in the background and after some tolerable time will take the nearest match even if it's not ideal.

The objective of "Quick Match" in most games is to get the player playing a multiplayer match as soon as possible. Hence "quick" match. It does this by&#x20;

1. Searching for an ideal match
2. If not found create an ideal lobby that others can join
3. If not enough join in a tolerated time joining the next best lobby it can find

### Lobby Browser

Another approach used is to display a list of "near match" lobbies to the user along with a "create lobby" button.

Older games didn't let you create a new lobby until you searched for one. Once the search failed it would display the nearest matches to your search arguments along with a create button. The idea here is a player should first fill up a waiting session or if none suits the player's needs create one of their own.

This model does much the same as Quick Match but lets the player decide what the "nearest match" lobby is. The downside to this is some players will be stubborn and always make their lobby increasing the average time to match for all players.

#### How to display lobbies

The [5 Lobbies](broken-reference) sample scene demonstrates browsing for lobbies. If you wanted to do this model the ideal solution is to let the user define their search arguments and return a small number of the lobbies if any that match that say the top 10.&#x20;

You can then do searches that are slightly less strict ... what this means depends on your game. For example let's say your game is a classic shooter with modes like CTF, C\&H, and KofH and has session sizes of 4v4, 8v8 and 16v16 and maybe also lets your players pick a map.

Your player may search for CTF 4v4 on map X. You return the top 10 matches that suit that but show the player the top 10 CTF 8v8, top 10 C\&H 4v4, top 10 KofH 4v4, etc. You don't want to flood your player with too many options and you don't want to bury their preference the idea is to show them options in case their ideal match isn't available or in case they didn't think to look for something else.

### I need to list all servers

{% hint style="success" %}
A lobby is not a server

A lobby is a group of players looking to play a game together.
{% endhint %}

It's keenly important that you understand that a lobby is not a server, it is not a networking concept at all. It is a chat room where players meet and converse to decide what they would like to play together before they go do so.

You can think of it like jumping on Team Speak, Discord, etc. and rounding up a few friends to go play a game together.

If you want to list a set of available servers then you 1st off need servers. You can look at creating a server build for your game and having it register as a [Steam Game Server](game-server-browser/).

{% hint style="info" %}
Learn more [here](game-server-browser/)
{% endhint %}

Once you have a server build you need to decide how you going to host it.

1.  Player Hosted

    This is where you ship your server build and let players host it themselves
2.  Bespoke

    Services like [G-Portal](https://www.g-portal.com/) can be used to host official, private, etc. ... you see this done a lot with survival games like Minecraft, Conan Exiles, etc.
3.  Traditional

    Using a service like [PlayFab](https://playfab.com/), [GameSparks ](https://www.gamesparks.com/)or [Multiplay](https://unity.com/products/multiplay)
4.  DIY

    Do it yourself, if your a glutton for pain or just really like data operations you could of course host your servers your self.

Doing this will let you browse for and display all available (and publicly visible) stem game servers via a [Steam Game Server Browser](../../../../toolkit-for-steamworks/unity/components/game-server-browser-manager.md).

## Steam Game Server

[Steam Game Server Game Data](../../../../toolkit-for-steamworks/unity/classes-and-structs/steam-settings/game-server.md#gamedata) configurations can be used to establish a similar set of "metadata" as used by the Lobby Matchmaking system. The [Steam Game Server Browser](../../../../toolkit-for-steamworks/unity/components/game-server-browser-manager.md) can be used to query for specific game servers again like searching for a Steam Lobby. The principle difference between the Steam Game Server system and the Lobby system is that Steam Game Servers are relatively permanent and can be browsed as a full list, in contrast, a Lobby is effectively a chat room and highly temporary.&#x20;
