# Unity Configuration

Open your Project Settings and select Player > Discord.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

When you first do this, it will create a DiscordSocialSettings object in your project's Settings folder.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

This is used with the [Initialise Discord Social component script](../initialization/unity-initialization.md#component). It is not a requirement to use it if you prefer to go "Pure Code" as described in the [initialisation](../initialization/unity-initialization.md#pure-code-1) step.

## Discord Event Triggers

Platform SDKs like Discord Social SDK have a host of system-level events. All of these are exposed on the main static class `DiscordSocialApp`. In addition, we have provided an easy-to-use component script that exposes them all to you in the Unity Inspector as well.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### Activity Invite Created

Triggered when another user sends the local user an invite to join a Discord activity (e.g., game session or lobby).\
Useful for showing in-game UI notifications or prompting the player to accept or reject the invite.

***

### Activity Invite Updated

Fires when an existing invite is updated, typically with new context like an updated game session or changed activity state.\
Use this to refresh any UI that displays pending invites.

***

### Authorize Result

Occurs after an OAuth authorization attempt completes, providing the result, authorization code, and redirect URI.\
This is useful for custom handling of OAuth flows, e.g., redirecting the user or logging the result.

***

### Connect

Fired when a connection to the Discord client has been successfully established.\
Great for enabling features that require a live Discord link, like rich presence or lobby features.

***

### Disconnect

Fires when the SDK disconnects from Discord, either intentionally or due to a failure.\
Use this to disable Discord-dependent features or notify the player of disconnection.

***

### Lobby Created

Triggered when a lobby is successfully created or joined.\
Useful for initializing lobby UI, assigning player slots, or beginning matchmaking sequences.

***

### Lobby Deleted

Fired when a lobby is closed or the user leaves it.\
Can be used to clean up lobby UI, reset state, or return players to a pre-lobby screen.

***

### Lobby Member Added

Occurs when a new user joins the current lobby.\
Use this to populate UI elements, such as player cards or status indicators.

***

### Lobby Member Removed

Triggered when a member leaves or is removed from the lobby.\
Use this to update the lobby UI, show exit notifications, or enforce minimum player requirements.

***

### Lobby Member Updated

Fired when a member’s metadata (e.g., team assignment, ready state) changes.\
Great for reacting to player readiness, roles, or custom user data stored in the lobby.

***

### Lobby Message Deleted

Occurs when a message is deleted from a lobby chat channel.\
Used to update in-game chat UIs to reflect deleted messages.

***

### Lobby Message Received

Fired when a new message is received in a lobby's chat channel.\
Use this to display chat messages, ping the user, or play message alerts.

***

### Lobby Message Updated

Triggered when a lobby chat message is edited.\
Can be used to refresh or annotate updated messages in the chat UI.

***

### Lobby Updated

Occurs when the current lobby's metadata or configuration is changed.\
Useful for syncing the lobby’s public info, like name, mode, or visibility status.

***

### Message Created

Fired when a new message is created in any Discord context, such as DMs or other channels.\
Helpful for global message monitoring features or aggregating chat activity.

***

### Message Deleted

Triggered when a message is deleted from a channel or DM.\
Use this to maintain accurate message history or show message removal notices.

***

### Message Updated

Occurs when a message is edited in a channel or DM.\
Can be used to update message displays or highlight edited content.

***

### Participant Changed

Fired when a voice chat participant joins or leaves. Includes speaking status.\
Use this for showing who's in the voice channel, who's currently speaking, or managing audio indicators.

***

### Ready

Fired when the SDK is fully initialized and connected, indicating the client is operational.\
Ideal for triggering startup logic like presence setup or loading Discord-related features.

***

### Received Token

Occurs when an access token is successfully retrieved, typically following an authorization process.\
Use this to store or validate credentials before continuing with user session setup.

***

### Relationships Created

Fired when a new friend or relationship is added.\
Use this to sync friend lists or trigger friend-related in-game features.

***

### Retrieve Token Failed

Occurs when token retrieval fails, such as during OAuth or provisional token flows.\
Can be used to present retry options or fallback authentication mechanisms.

***

### Status Changed

Fires whenever the connection status changes (e.g., from Connecting to Ready). Includes error info if applicable.\
Ideal for updating UI indicators or triggering logic based on current connection state.

***

### Token Expiration

Occurs when the current authentication token expires.\
Common with provisional tokens which have short lifespans.\
Use this to refresh tokens or prompt the user to reauthenticate.

***

### User Message Deleted

Fires when a message sent by or to the current user is deleted.\
Used to maintain accurate history in personal chat UIs.

***

### User Message Received

Triggered when a new direct message is received by the local user.\
Use this to notify the player, update chat logs, or trigger audio/visual alerts.

***

### User Message Updated

Fired when a DM sent to the user is edited.\
Used to refresh message content in direct chat views.

***

### User Updated

Occurs when the current user's Discord profile changes — avatar, name, status, etc.\
Useful for syncing UI with updated user data or refreshing cached user profiles.

***

### Voice State Changed

Triggered when a participant's voice state (muted, deafened, etc.) changes.\
Use this to reflect real-time voice statuses in-game, like mute icons or speaker indicators.
