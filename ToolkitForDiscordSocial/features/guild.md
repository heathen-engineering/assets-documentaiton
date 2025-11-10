# Guild

The Social SDK uses the term **Guild** to represent what everyone else calls a **Discord Server**. Unfortunately, the name can be confusing since a Guild here is simply a Discord Server — nothing more, nothing less.

## What is it?

* **Just a Discord Server:**\
  When you get the list of Guilds, you’re simply retrieving all the Discord servers the local user is a member of. There’s no special or unique meaning behind the term.
* **Limited Server Info:**\
  You can get the server’s **name**, but not its image or icon, through the SDK.
* **Channels Are Included:**\
  Each Guild gives you access to the list of channels the user can see within that server. These channels indicate whether they can be linked to a lobby.

### How Channels and Lobbies Relate

* **Finding Channel IDs:**\
  You can use the Guild’s channels to find the **channel ID** needed to link a lobby to a channel.
* **Linking Lobbies to Channels:**\
  This linking bridges a temporary chat lobby to a persistent server channel, allowing in-game chat to sync with Discord channel conversations.
* **No Lobby Secret Exposure:**\
  The SDK doesn’t provide access to the lobby secret associated with a linked channel. This secret string is required to join a lobby, so the user must share it outside the SDK for you to join.

## Use Case

### Guild Data

* **Player Discord Server Setup:**\
  This data can be used in a Discord integration UI to let players choose their Discord servers and channels to link lobbies to.
* **Channel Visibility & Linking:**\
  Channels expose whether they can be linked to a lobby, letting you filter and present valid chat channels for integration.
* You cannot chat on a channel directly; you chat through lobbies, so to chat on a channel, you would need to be a member of its lobby, if any.
