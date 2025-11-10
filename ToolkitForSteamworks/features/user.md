# User

Steam Friends is a core component of the Steam platform that enhances the social experience of gaming by connecting players in real time. In this article, we’ll explore the Steam Friends interface provided by the Steamworks SDK, which offers a rich set of features for managing user profiles, friend lists, game invitations, and in-game communication. Whether you’re looking to integrate friends’ status updates or create custom matchmaking experiences, understanding Steam Friends is essential for creating a more connected and engaging game environment.&#x20;

## Examples

### User Profile

Steam provides a lot of rich information about your friends, and this can be used in-game for many purposes, such as a visually rich display for your local user and or the other players they are playing with.

<figure><img src="../.gitbook/assets/image (294).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the User modular component to work with user data in your game. Modular components start empty and can be tailored to the specific need.

<figure><img src="../.gitbook/assets/image (408).png" alt="Empty User component"><figcaption><p>Empty User component</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (418).png" alt=""><figcaption><p>User component with Avatar, Hex (Input Field), Level, Name and Status as shown in the example image above</p></figcaption></figure>

### Local User

When true, the player (local user) data will be loaded; otherwise, you will need to set the user you want it to load, such as from a lobby member list, friend list, etc.

### Fields

Using the Fields control, you can add fields that will be set based on the loaded user. That is, if you add an Avatar, then set the user from, say, your friends list, it will get that friend's avatar and update the image you reference.

<figure><img src="../.gitbook/assets/image (417).png" alt=""><figcaption></figcaption></figure>

### Configuration

Using the configuration control, you can toggle on and off additional functionality such as Events and Invite options.

<figure><img src="../.gitbook/assets/image (419).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
//Assumes
UserData user; //= This is the user you want to read data for
//For the local user UserData.I can be used in such as
string name = UserData.Me.Name;

// Examples of getting each of the relevant fields
string name = user.Name;
string nickname = user.Nickname;
user.LoadAvatar(image =>
{
    //image is the Texture2D you can use
});
EPersonaState status = user.State;
int level = user.Level;
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprints

The following nodes can be used to gather detailed information about the current user

<figure><img src="../.gitbook/assets/image (298).png" alt=""><figcaption></figcaption></figure>

The following nodes can be used to gather detailed information about another user

<figure><img src="../.gitbook/assets/image (297).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (351).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
//Get the UTF8 name
const char* RawName = SteamFriends()->GetFriendPersonaName(CSteamID(static_cast<uint64>(int64Value)));
//Convert to Unreal's FString
FString StringName = FString(FUTF8ToTCHAR(RawName));

//Similar for getting the local user's persona name, but we have a shortcut
FString LocalName = FString(FUTF8ToTCHAR(SteamFriends()->GetPersonaName()));

//Get Steam Level
int32 IntLevel = SteamFriends()->GetFriendSteamLevel(CSteamID(static_cast<uint64>(int64Value)));

//And the shortcut for the local user
int32 LocalLevel = SteamUser()->GetPlayerSteamLevel();

//Getting an avatar image is a more involved process, first, we ask Steam to cash
//The data locally and give us a handle on it
int Handle = SteamFriends()->GetLargeFriendAvatar(CSteamID(static_cast<uint64>(int64Value)));

//Now we need something to load the data into
UTexture2D* AvatarTexture = UTexture2D::CreateTransient(STEAMWORKS_AVATAR_SIZE, STEAMWORKS_AVATAR_SIZE, PF_R8G8B8A8);
//This part is optional, but usually, it adds this object to the root so it doesn't get GCed
//Only do this if you are managing the references' life as we do, such as by cashing it 
//in a sub-system for faster fetch later
AvatarTexture->AddToRoot();

//Finally, we load the data
check(Handle > 0);
check(AvatarTexture != nullptr);

TArray<uint8> Buffer;
Buffer.SetNumZeroed(STEAMWORKS_AVATAR_BYTE_SIZE);

//copy it directly within this call
if (SteamUtils()->GetImageRGBA(Handle, Buffer.GetData(), Buffer.Num()))
{
    void* MipData = AvatarTexture->GetPlatformData()->Mips[0].BulkData.Lock(LOCK_READ_WRITE);
    FMemory::Memcpy(MipData, Buffer.GetData(), Buffer.Num());
    AvatarTexture->GetPlatformData()->Mips[0].BulkData.Unlock();

    AvatarTexture->GetPlatformData()->SetNumSlices(1);
    AvatarTexture->NeverStream = true;

    AvatarTexture->UpdateResource();
}
else
{
    ensure(false && "this shouldn't happen");
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
//Get the local user's name
string name = SteamFriends.GetPersonaName();
//Get another user's name
string name = SteamFriends.GetFriendPersonaName(userId);

//To get the user's avatar image, it is a two-step process
//First, get the handle
int32 handle = SteamFriends.GetLargeFriendAvatar(userId);

//Set up buffers to hold the data
int bufferSize = (int)(width * height * 4);
byte[] imageBuffer = new byte[bufferSize];

//Load and use the data
if (SteamUtils.GetImageRGBA(imageHandle, imageBuffer, bufferSize))
{
    //Now use it how you like
}
```
{% endtab %}
{% endtabs %}



### Friend List

Tools for querying the list of friends are available and allow you to create detailed visual friend lists using your engine of choice's built-in UI tools.

<figure><img src="../.gitbook/assets/image (295).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Use the Friend List component to get a list of the local user's (player's) friends and display those friends to a target transform.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Include Followed

A little-used feature, this will expand the search to include Clans the user is following. The Steam Clan aka Steam Group feature is not currently well supported by Valve but is included for completeness' sake.

### Filter

Specify the sub-set of the user's friends you would like to have returned if any.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

### Content & Record Template

Content is simply the Transform you want the tool to spawn objects to. This would typically be a Layout Group control such as Unity's built in Vertical Layout Group.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

#### Record Template

The Record Template is the object that will be spawned for each user found. This should contain a "User" component as demonstrated in the [User Profile](user.md#user-profile) example.

## C\#

```csharp
//Get an array of the player's friends
UserData[] myFriends = UserData.MyFriends;

//You can now loop through that list and read the profile information
foreach(var friend in myFriends)
{
    //Get the name and whatever else you might like to do with it
    string name = friend .Name;
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Get an array of the user's friends

<figure><img src="../.gitbook/assets/image (299).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
EFriendFlags eFlag = EFriendFlags::k_EFriendFlagImmediate;
int count = SteamFriends()->GetFriendCount(eFlag);
TArray<int64> results;

for (int i = 0; i < count; i++)
{
    results.Add(static_cast<int64>(SteamFriends()->GetFriendByIndex(i, eFlag)).ConvertToUint64());
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
EFriendFlags flags = EFriendFlags.k_EFriendFlagImmediate;
var count = SteamFriends.GetFriendCount(flags);
if (count > 0)
{
    var results = new CSteamID[count];
    for (int i = 0; i < count; i++)
    {
        results[i] = SteamFriends.GetFriendByIndex(i, flags);
    }

    //results is now an array of CSteamID
}
```
{% endtab %}
{% endtabs %}

### Invite to Game

You can invite a friend to play a game with you, Note this is inviting them to a connection string, not a lobby. It is possible to invite a friend to a lobby as well, We will explain that in the Lobby article.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not applicable.

## C\#

Invite the user to the game

```csharp
//Given a UserData, such as read from your friends list
UserData myFriend;

//With a valid friend, we can simply "Invite To Game", sending them 
//A connection string which can be anything you need it to be
myFriend.InviteToGame("whatever connection string you need");
```

The user will see the invite in their Friend chat and can accept the invite there. When they accept the invite, what happens next depends on whether or not they are currently playing this game.&#x20;

If they are playing this game, then the Rich Presence Join Requested event will be raised. You can listen to this event via our Steamworks Event Triggers

<figure><img src="../.gitbook/assets/image (300).png" alt=""><figcaption></figcaption></figure>

Or you can listen in code

```csharp
using Heathen.SteamworksIntegration.API;

Overlay.Client.EventGameRichPresenceJoinRequested.AddListener(HandleJoinRequest);

private void HandleJoinRequest(UserData whoInvitedYou, string connectionStringTheyPassed)
{
    //Handle the event
}
```

If the user was not already playing the game when they clicked the Accept button. Then, Steam will launch the game with the connection string on the command line. Valve doesn't document this well, but this code should get you going with reading the command line value.

```csharp
// Get all command-line arguments
string[] args = Environment.GetCommandLineArgs();
        
// Loop through each argument to find one that starts with "connect="
foreach (string arg in args)
{
    if (arg.StartsWith("connect="))
    {
        // Extract and return the connection string (everything after "connect=")
        return arg.Substring("connect=".Length);
    }
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

You can invite a friend with the Invite to Game node

<figure><img src="../.gitbook/assets/image (301).png" alt=""><figcaption></figcaption></figure>

When the user accepts the invite, one of two things will happen.

If they are already in the game then the Rich Presence Join Requested event will be raised. You can find this on your Steam Game Instance

<figure><img src="../.gitbook/assets/image (302).png" alt=""><figcaption></figcaption></figure>

If they are not already in-game, then you would read the value from the command line

<figure><img src="../.gitbook/assets/image (303).png" alt=""><figcaption></figcaption></figure>

The string value will be empty if none is found, or will be the connection string if one is found.

## C++

```cpp
//Assuming
CSteamID userId; //= who to invite
FString connectionString; //= where to send them

//To send the connection string
SteamFriends()->InviteUserToGame(steamId, StringCast<ANSICHAR>(*connectionString).Get());

//To get the connection string from the command line
FString ConnectString;
// FParse::Value will search the command line for "connect=" and extract its value.
if (FParse::Value(FCommandLine::Get(), TEXT("connect="), ConnectString))
{
	UE_LOG(LogTemp, Log, TEXT("Connection string found: %s"), *ConnectString);
	// Use ConnectString to join the game session or perform further processing.
}
else
{
	UE_LOG(LogTemp, Log, TEXT("No connection string found."));
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
To invite a friend to your game

```csharp
//Assume
CSteamID userId;         //=Is the friend to invite
string connectString;    //=Is the connection string to send them

SteamFriends.InviteUserToGame(userId, connectString);
```

When the friend accepts the invite, if they are currently in game, then the Rich Presence callback will be invoked. You need to create and manage that somewhere it won't be GCed.

```csharp
//Declare the callback somewhere safe
Callback<GameRichPresenceJoinRequested_t> m_RPJoinRequested_t;

//Don't forget to "create" it, pointing it at a function to call when invoked
m_RPJoinRequested_t = Callback<GameRichPresenceJoinRequested_t>.Create(HandlerFunction);
```

Your handler function would look similar to this

```csharp
void HandlerFunciton(GameRichPresenceJoinRequested_t arg0)
{
    // arg0.m_steamIDFriend is the friend who invited you
    // arg0.m_rgchConnect is the connection string they sent
}
```
{% endtab %}
{% endtabs %}

