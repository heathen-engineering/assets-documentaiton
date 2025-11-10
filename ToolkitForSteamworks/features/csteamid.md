# CSteamID

Here we will explain in detail the nature and structure of Valve's CSteamID and how to use it. Its worth noting that our Toolkit for Steamworks provides you with tools and features that should mean you rarely need to work with raw Steam IDs; however, it is useful to understand them.

Valve's CSteamID, also known simply as "Steam ID" is a ulong value (64 bits) and is used by Steam API to uniquely identify ... well, most things.&#x20;

The native CSteamID ulong value is composed of 4 main parts

### Universe

```csharp
namespace Steamworks
{
    public enum EUniverse
    {
        k_EUniverseInvalid = 0,
        k_EUniversePublic = 1,
        k_EUniverseBeta = 2,
        k_EUniverseInternal = 3,
        k_EUniverseDev = 4,
        k_EUniverseMax = 5
    }
}
```

### Type

```csharp
namespace Steamworks
{
    public enum EAccountType
    {
        k_EAccountTypeInvalid = 0,
        k_EAccountTypeIndividual = 1,
        k_EAccountTypeMultiseat = 2,
        k_EAccountTypeGameServer = 3,
        k_EAccountTypeAnonGameServer = 4,
        k_EAccountTypePending = 5,
        k_EAccountTypeContentServer = 6,
        k_EAccountTypeClan = 7,
        k_EAccountTypeChat = 8,
        k_EAccountTypeConsoleUser = 9,
        k_EAccountTypeAnonUser = 10,
        k_EAccountTypeMax = 11
    }
}
```

### Account Id

```csharp
AccountId_t accountId;
```

The data type AccountId\_t is a wrapper around the uint primitive type ... that is it is a uint value with a few extra features.

### Account Instance

```csharp
uint unAccountInstance;
```

This value is readable on the CSteamID but not documented in Steam.&#x20;

We know from reviewing the CSteamID struct and its various methods that for Type Clan and GameServer, the account instance is set to&#x20;

```csharp
unAccountInstance = 0u;
```

For all other types, Steam sets the value to&#x20;

```csharp
unAccountInstance = 1u;
```

We know from experience that attempting to set a lobby in this way will fail, resulting in an invalid lobby. We have deduced that lobbies (seem) to have a constant account instance value of

```csharp
unAccountInstance = 393216u;
```

## Examples

{% tabs %}
{% tab title="Toolkit for Unity" %}
Heathen has created wrap-around structures like UserData and Lobby that are interchangeable with CSteamID and ulong and provide helpful features unique to each use case of the ID. In most cases, you should be using UserData, Lobby, Clan, etc. and not need to bother with the raw CSteamID or its ulong value.

Steam IDs are used for a lot of different things and each has its own set of features and functions. For example, a CSteamID can represent a user and users have additional features like name, nickname, rich presence, etc. Alternatively, a CSteamID could represent a lobby which has features like metadata, members, etc.

Heathen has created a set of wrappers that let you treat each ID as a unique type and simplify working with the features of each unique type. Note each of these is implicitly convertible ... that is, you can use them as if they are CSteamID\_t or ulong and you can assign them from CSteamID\_t or ulong. These also have additional handlers to help you work with them as AccountID\_t

### ClanData

This is for IDs that represent a "clan" or "group"

### LobbyData

This is for IDs that represent lobbies, aka chats

### UserData

This is for IDs that represent users

### Creating Steam IDs

While the full CSteamID is a 64-bit long, its a not very human-friendly number the actual "unique" part is just 32-bits long and much more manageable by a human. If you know the "type" of the ID then you can reconstruct it providing only the 32-bit "Account ID" part also known as a "Friend ID".

#### Adding Friends

Let's say you want your users to be able to "invite" each other to become friends through some method outside of Steam, such as chat, stream, etc. You could simply show the user their "Friend ID", aka the Account ID of their CSteamID. They can provide this fairly short number to prospective friends.

To display the local user's Friend ID, we can simply read it from the local user's User Data.

```csharp
textField.text = UserData.Me.FriendId.ToString();
```

This will populate a simple number in the provided text field.

You can then also provide an input field where users can type in the IDs they get from others. The friend ID typed in can then be used to construct a UserData object which you can use for anything you like, including adding to Friends.

```csharp
//Parse the input string to a uint value
uint FriendID = System.Convert.ToUint32(inputfield.text);
//Get the UserData for this friend ID
UserData newGuy = UserData.Get(FriendID);
//Invite this user to be our friend on Steam
API.Overlay.Client.Activate(FriendDialog.friendadd, newGuy);
```

We even have a shortcut you can use to do this all in 1 line

```csharp

if(UserData.AddFriend(inputField.text))
{
    //text was parsed to a uint value and sent to Steam
}
else
{
    //text is not a unit value, and no action was taken
}
```

#### Sharing Lobbies

Let's say you want to share a simple string so that players can join lobbies automatically. You could do this in a few ways but one option is to share the lobbies, and one is to expose the lobby's account ID.

```csharp
lobbyIdField.text = myLobby.AccountId;
```

As with the Add Friend example, you can then join a lobby via the ID

```csharp
//Parse the input string to a uint value
uint LobbyAccountID = System.Convert.ToUint32(inputfield.text);
//Get the UserData for this friend ID
Lobby newLobby = Lobby.Get(LobbyAccountID );
//Invite this user to be our friend on Steam
mewLobby.Join(CallbackHandler);
```

This can even be done in 1 line

```csharp
if(Lobby.Join(inputfield.text, CallbackHandler))
{
    //input text was parsed and sent to Steam
}
else
{
    //Invalid input text, no action taken
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
All Steam IDs can be expressed as simple value types, such as int64 for Steam ID. Heathen provides several Blueprint nodes that help translate the IDs into and out of various data types, such as Hex strings.

See the Steam ID Tools article for more information.

<figure><img src="../.gitbook/assets/image (287).png" alt=""><figcaption></figcaption></figure>

### C++ <a href="#unreal-steamid-tips" id="unreal-steamid-tips"></a>

Working in C++ means you are working with the native CSteamID object, which has methods for getting the Account ID and other parts of the ID. For example, if you wanted to convert an ID to a human-friendly Hex value

```cpp
FString::Printf(TEXT("%X"), id.GetAccountID());
```

Assuming the id was a CSteamID this would get the unique part of that ID, the account id and print it to a hex-style string.&#x20;

You can do the inverse, then assuming `Fstring hexFriendId`, then

```cpp
FString HexValue = hexFriendId.Replace(TEXT("0x"), TEXT(""), ESearchCase::CaseSensitive);
int Result = FCString::Strtoi(*HexValue, nullptr, 16);

// Handle overflow or conversion errors
if (Result == 0 && HexValue != TEXT("0"))
{
    UE_LOG(LogTemp, Warning, TEXT("Hexadecimal string conversion overflow or error."));
}

CSteamID steamId(Result, EUniverse::k_EUniversePublic, EAccountType::k_EAccountTypeIndividual);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Details Coming Soon
{% endtab %}
{% endtabs %}
