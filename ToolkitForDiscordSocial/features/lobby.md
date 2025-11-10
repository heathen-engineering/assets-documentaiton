# Lobby

Discord’s Social SDK uses the term **Lobby**, but it doesn’t match the traditional idea of a multiplayer game lobby. Instead, think of a Lobby more like a **temporary chat group or DM group** that exists to facilitate chat and voice between a small set of users.

## What is it?

* **More a Chat Group than a Game Lobby:**\
  Unlike conventional game lobbies, Discord lobbies don’t have built-in matchmaking, server connection info, or discovery. They’re primarily ephemeral chat spaces for voice, text, and presence.
* &#x20;**Can Be Linked to a Server Channel:**\
  A lobby can be linked to a Discord server’s text or voice channel. This lets you bridge chat between your game and Discord, enabling cross-platform conversations.
* **Static Metadata Only at Creation:**\
  You can assign metadata key-value pairs to a lobby, but only when you create it. This metadata is static and **cannot be updated afterwards** through the Social SDK. No **Matchmaking or Discovery:**\
  There’s no way to search, filter, or find lobbies. Joining is either by invitation or by requesting to join a friend’s lobby.

### Lobby Members and Metadata

* **Members Can Have Dynamic Metadata:**\
  Each member in a lobby can store their metadata, which **can be updated at runtime**. This lets you track per-user info like status or preferences while they’re in the lobby.
* **Member Metadata Is Not Searchable:**\
  This data is purely key-value and doesn’t support matchmaking or discovery features.

## Use Case

### Discord Chat Integration

The core utility of Discord lobbies in the Social SDK is to **expose Discord chat within your game**, whether:

* Creating temporary chat groups akin to Discord DMs, or
* Linking to existing Discord server channels to enable seamless cross-platform chat.

Because lobbies lack matchmaking or server connection features, they function best as **social spaces** rather than game session hosts.

## Examples

### Create or Join

To create or join a Discord lobby, you need to know its **secret**.

**What is a secret?**\
It’s simply a string that identifies the lobby. Think of it as the lobby’s “name,” but it must be globally unique—typically a GUID or similarly complex identifier.

While you _can_ use a human-friendly secret, be cautious: simpler or predictable strings increase the risk of abuse or unwanted joins. In practice, unique and complex secrets are far safer.

To make joining easier without sharing secrets manually, you can leverage Discord’s **Invite** and **Request to Join** features. These allow players to join each other’s lobbies seamlessly without needing to type or share the secret directly.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Coming Soon

## C\#

For all asynchronous calls, we have exposed 3 approaches for you to work with. You can choose whichever suits you best; they all ultimately do the same thing.&#x20;

If you wonder which is "best", the original "callback" approach is the most performant and flexible option.

```csharp
DiscordSocialApp.CreateOrJoinLobby(secret, callback);
```

### secret

A unique string that will be used to join this lobby by other users. It's generally best practice to make this a globally unique value.

### callback

A delegate to be invoked when the process is complete. This can be a function name or a lambda expression.

Example:

Let's assume you have a function such as

```csharp
void HanleLobbyCreated(ClientResult result, ulong lobbyId)
{
    // Do something with your lobby
}
```

Then you could

```csharp
string secret = Guid.NewGuid().ToString();
DiscordSocialApp.CreateOrJoinLobby(secret, HandleLobbyCreated);
```

Alternatively, we can do the same thing with an anonymous function.

```csharp
string secret = Guid.NewGuid().ToString();
DiscordSocialApp.CreateOrJoinLobby(secret, (result, lobbyId) =>
{
    // Do something with your lobby
});
```

***

### Task Option

You can do the same using traditional threading tasks if you prefer that paradigm.&#x20;

{% hint style="warning" %}
System.Task will cause a small amount of GC allocation. This is not generally a concern with infrequent things, such as creating a lobby, but it is worth knowing.

Using tasks in this manner also causes blocking.
{% endhint %}

```csharp
string secret = Guid.NewGuid().ToString();
var (result, lobby) = await DiscordLobbyData.CreateOrJoinTask(secret);
```

***

### UniTask Option

You can do the same using UniTask if you prefer that paradigm.

{% hint style="warning" %}
Cysharp.Threading.Tasks create fewer GC allocations, but will still cause GC allocations in some cases, depending on the data types being worked with.

Using tasks in this manner also causes blocking.
{% endhint %}

```csharp
string secret = Guid.NewGuid().ToString();
var (result, lobby) = await DiscordLobbyData.CreateOrJoinUniTask(secret);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}

{% endtab %}
{% endtabs %}

### Invite User

To invite a user, you must have an [Active Lobby](lobby.md#get-and-set-active-lobby); Discord will use that lobby as the target of the invite.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Coming Soon

## C\#

Give the user you wish to invite to your [Active Lobby](lobby.md#get-and-set-active-lobby).

```csharp
DiscordUserData user;
```

You can invite them via

```csharp
user.Invite(content, callback);
```

### content

This is not currently used according to the SDK, but it is included, so we have added it. Just pass an empty string for now.

### callback

This is a delegate that will be invoked when the process completes.

Example:

```csharp
void HandleInviteSent(ClientResult result)
{
    // The invite was sent, check the result for status
}
```

You can then do

```csharp
user.Invite(string.Empty, HandleInviteSent);
```

or using lambda

```csharp
user.Invite(string.Empty, result =>
{
    // The invite was sent, check the result for status
});
```

### Task

```csharp
var result = await user.InviteTask(string.Empty);
```

### UniTask

```csharp
var result = await user.InviteUniTask(string.Empty);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Get and Set Active Lobby

Invite and Request features of lobby work with the "active" lobby being the one set on the user's Rich Presence for this application. A user may be a member of many lobbies, but only 1 will be "active".

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Coming Soon

## C\#

You can monitor the current active lobby via

```csharp
bool hasActiveLobby = DiscordLobbyData.Active.HasValue;
DiscordLobbyData activeLobby = DiscordLobbyData.Active.Value;
```

You can set a lobby as active in a similar manner ...&#x20;

```csharp
ulong lobbyId; // If you only have the ID, you can get the data
DiscordLobbyData myLobby = lobbyId; // it implictly converts
```

```csharp
myLobby.MakeActive(maxSize, message, platforms, callback);
```

### maxSize

Lists the maximum number of users expected in the lobby

### message

optional status message for the resulting Activity

### platforms

An enum that lists the supported platforms for this activity

### callback

A delegate to be invoked when the process is complete

### Example:

```csharp
void HandleMadeActive(ClientResult result)
{
    //It's all done, use the result to check the status
}
```

You can then call\


```csharp
int maxSize = 42;
string message = "Hello World";
ActivityGamePlatforms platforms = 
ActivityGamePlatforms.Desktop | ActivityGamePlatforms.Xbox | ActivityGamePlatforms.PS5;
myLobby.MakeActive(maxSize, message, platforms, HandleMadeActrive);
```

Or using lambda&#x20;

```csharp
myLobby.MakeActive(maxSize, message, platforms, result =>
{
    //It's all done, use the result to check the status
});
```

### Task

{% hint style="warning" %}
System.Task will cause a small amount of GC allocation. This is not generally a concern with infrequent things, such as creating a lobby, but it is worth knowing.

Using tasks in this manner also causes blocking.
{% endhint %}

```csharp
var result = await myLobby.MakeActiveTask(maxSize, message, platforms);
```

### UniTask

{% hint style="warning" %}
Cysharp.Threading.Tasks create fewer GC allocations, but will still cause GC allocations in some cases, depending on the data types being worked with.

Using tasks in this manner also causes blocking.
{% endhint %}

```csharp
var result = await myLobby.MakeActiveUniTask(maxSize, message, platforms);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Request to Join

You can request to join a user assuming they have a valid [Active Lobby](lobby.md#get-and-set-active-lobby).

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Coming Soon

## C\#

Assuming a user you wish to join

```csharp
DiscordUserData user;
```

You can then

```csharp
user.RequestToJoin(callback);
```

### callback

This is a delegate to be invoked when the process is complete.

Example:

assuming

```csharp
void HandleRequestToJoinSent(ClientResult result)
{
    // The request was sent.
}
```

Then

```csharp
user.RequestToJoin(HandleRequestToJoinSent);
```

or using lambda

```csharp
user.RequestToJoin(result =>
{
    // The request was sent.
});
```

### Task

{% hint style="warning" %}
System.Task will cause a small amount of GC allocation. This is not generally a concern with infrequent things, such as creating a lobby, but it is worth knowing.

Using tasks in this manner also causes blocking.
{% endhint %}

```csharp
var result = await user.RequestToJoinTask();
```

### UniTask

{% hint style="warning" %}
Cysharp.Threading.Tasks create fewer GC allocations, but will still cause GC allocations in some cases, depending on the data types being worked with.

Using tasks in this manner also causes blocking.
{% endhint %}

```csharp
var result = await user.RequestToJoinUniTask();
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Coming Soon
{% endtab %}
{% endtabs %}
