# Features Overview

The Discord Social SDK (also known as Discord Partner SDK) introduces several concepts that, at first glance, can be confusing due to their naming. Here’s a clear rundown of the core features and what they represent:

## User

The simplest and most intuitive concept.

* Represents a Discord user with an ID, username, and avatar.
* Exactly what you’d expect.

## Lobby

Despite the name, a Lobby is **not** a traditional game lobby.

* More like a temporary **DM group** or chat room between users.
* Can be linked to a server channel but is otherwise ephemeral.
* Primarily used for chat, voice, and presence integration within a small group.
* Metadata exists but is statically created at the time of creation and can't be updated after that.
* Cannot be used for matchmaking; there is no search or filtering. You can either be invited to a lobby or ask to join your friend who has a lobby.
* Members in a lobby do have metadata that can be updated at run time.

## Guild

Simply a **Discord Server**.

* A persistent community that a user is a member of.
* The SDK currently supports listing your guilds but exposes limited server details.

## Channel

A **text or voice channel within a Discord server** (Guild).

* Channels can be linked to Lobbies to integrate game social features with server channels.
* Channels are persistent and part of the broader server structure.

## Call

A **voice connection state** associated with a Lobby or a Server Channel.

* Not a separate entity, but the state when voice chat is active in a channel or lobby.
* Provides voice communication capability within the SDK.

## Rich Presence (Activity)

Not truly “Rich Presence” as you might expect.

* Represents the user’s current **Activity** within the app/game.
* Carries metadata like join secrets and party info to enable invites and join requests.
* Limited to the app context and does not cover full presence or game state.
