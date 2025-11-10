# Users

In the Discord Social SDK, the **User** represents an individual Discord account and serves as a core building block for social interactions within your game or app.

## What is it?

A Discord User corresponds to a unique account on Discord, identified by a **Snowflake ID** — a large unsigned integer used across Discord to identify entities uniquely and globally.

&#x20;The User struct encapsulates essential data about the individual, including:

* **Username**: The chosen display name without discriminator.
* **Global Name**: A customizable display name introduced by Discord, which may differ from the username.
* **Display Name**: A convenient property that returns the most appropriate name for UI, often the global name if set, else the username.
* **Avatar URLs**: Static and animated avatar image URLs.
* **Status**: Online presence states like Online, Idle, Do Not Disturb, and Offline.
* **Provisional Status**: Whether the user is provisional (new or unverified).

### What Can it Do?

The User object enables several useful functions in social and multiplayer contexts:

* **Access User Metadata**: Retrieve display names, avatars, and status to represent users visually and contextually in your UI.
* **View Relationships**: Query friend lists, incoming/outgoing friend requests, and blocked users to build social features.
* **Load Avatars Asynchronously**: Fetch avatar images efficiently to display user profile pictures.
* **Rich Presence Activities**: Access and respond to a user’s current activity or game session.
* **Request to Join**: Send a join request to a user’s active game or lobby session if joinable.

## Use Cases

### Listing Friends

One of the primary uses of the Discord User object is to display your friend list within the game. You can retrieve the current user’s friends easily and show their names, avatars, and online status to create a social hub or invite system.

Example benefits:

* Show who is online or idle.
* Display avatars next to names for quick recognition.
* Allow inviting friends to a lobby or game session.

### Displaying Lobby Members

When your game uses Discord lobbies, you’ll want to display the members currently in the lobby. Using the User object, you can access each member’s display name, avatar, and status, whether they are friends or not. This enriches the social experience by showing real-time presence and recognisable identities.

Example benefits:

* Identify friends vs strangers in the lobby visually.
* Provide clickable profiles or invite options.
* Show user activity or game presence alongside their avatar.

## Examples

### List Friends

You can easily get a list of all the user's friends, and the status of those friends can let you know if they are online, offline, DND, etc. and if they are playing "this" game. You cannot, however, see if they are playing some other game.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

We have provided prefabs and their related component scripts to help you get and display the list of friends.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## C\#

You can fetch the list of friends via&#x20;

```csharp
List<DiscordUserData> friends = DiscordUserData.GetFriends();
```

Or via&#x20;

```csharp
List<DiscordUserData> friends = DiscordSocialApp.GetFriends();
```

With the list of your friends in hand, you can create whatever UI suits you.
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Coming Soon
{% endtab %}
{% endtabs %}

### User Avatar

You can get the static or animated avatar for a user.

{% tabs %}
{% tab title="Toolkit for Unity" %}
You can get the URL for the static or animated avatar for a user.&#x20;

## Code Free

We have provided you with easy-to-use free tools to get the static avatar and apply it to a Raw Image similar to our [Toolkit for the Steamworks Load Avatar](https://app.gitbook.com/s/kfE3ZAs6TeNW5sBM2C3i/features/user#friend-profile) feature.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

## C\#

Assume a user

```csharp
DiscordUserData user;
```

You can load its static Avatar directly to a Texture2D for use in Unity materials and UI.

```csharp
user.LoadStaticAvatar((r) =>
        {
            if (image == null)
                image = GetComponent<RawImage>();

            if (image == null)
                return;

            currentUser = user;

            image.texture = r;
            OnLoaded?.Invoke();
        });
```

If you wanted to get the animated avatar, you would need to choose a 3rd party GIF tool or write your own, but we do expose the URL for you.

```csharp
string url = user.AnimatedAvatarUrl;
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Coming Soon
{% endtab %}
{% endtabs %}

### User Name

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Similar to User Avatar, we have an easy-to-use component that will read the name for you and apply it to a TMPro Text field.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

## C\#

You can do the same in code, assuming a user.

```csharp
DiscordUserData user;
```

then

```csharp
string name = user.DisplayName;
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Coming Soon
{% endtab %}
{% endtabs %}
