# Overlay

## Events

### Game Lobby Join Requested

### Game Rich Presence Join Requested

Called when the user tries to join a game from their friends list or after a user accepts an invite by a friend with `userData.InviteToGame(connectString);` or `API.Friends.Client.InviteUserToGame(user, connectString);`.

{% hint style="info" %}
This callback is made when joining a game. If the user is attempting to join a lobby, then the callback [Game Lobby Join Requested](overlay.md#game-lobby-join-requested) will be made.
{% endhint %}
