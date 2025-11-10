# Authentication

## Quick Start

Steam Authentication allows your game to verify the identity of a user via Steam's backend services. It is commonly used for multiplayer games, server access control, and web API integration. The system issues authentication tickets that can be validated by other clients, game servers, or your own backend.

You should use Steam Authentication when:

* You need to verify a player's identity in multiplayer sessions.
* You want to authenticate users with your backend or web services.
* You're integrating with Steam Web API endpoints that require proof of identity.

You _don’t_ need to use Steam Authentication when:

* Your game is entirely single-player and doesn’t rely on server-side identity checks.
* You're using Steam only for basic platform features like achievements or cloud saves.

Authentication is handled entirely via Steamworks API and does not require any setup in the Steamworks Developer Portal.

## Examples

### Get Ticket

When requesting an authentication ticket, you must specify the _intended recipient_ of the ticket—this is referred to as the "identity." The identity is **who the ticket is for**, not who is generating it. This means you should provide the Steam ID of the server, user, or Web API key that will _receive and validate_ the ticket, not your own ID.

{% tabs %}
{% tab title="Tookit for Unity" %}
## Code Free

You can use the Authentication modular component to work with Authentication in your game.&#x20;

<figure><img src="../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

Add the Get Ticket setting to enable the Get Ticket features

<figure><img src="../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>

You can now call Get Ticket from other scripts or Unity Events, this will store the resulting data in the Authentication object for later use

Example

<figure><img src="../.gitbook/assets/image (438).png" alt=""><figcaption></figcaption></figure>

Options include

* Get Ticket for Game Server\
  This takes a Game Server component reference and generates a ticket for that server.
* Get Ticket for Lobby Owner\
  This takes a Lobby component reference and generates a ticket for that Lobby's owner
* Get Ticket for Lobby Server\
  This takes a Lobby component reference and generates a ticket for that Lobby's Game Server
* Get Ticket for User\
  This takes a User component reference and generates a ticket for that User
* Get Ticket for Web API\
  THis takes a string being the identity used by a given Web API and generates a ticket for that web API.

You can add the General Events component and make use of the Changed event which will be invoked when the ticket is ready to use.

<figure><img src="../.gitbook/assets/image (439).png" alt=""><figcaption></figcaption></figure>

Additionally you can add the RPC Invoke setting and make use of the RPC Invoked event. This will raise when the ticket is ready and will format the data in the manner typically used by HLAPI's such as NetCode for GameObjects, PurrNet, Mirror, FishNet, etc.

<figure><img src="../.gitbook/assets/image (440).png" alt=""><figcaption></figcaption></figure>

## C\#

To get a ticket for use by a User or Steam Game Server, you will provide that user's or server's ID

```csharp
// Remember, a UserData is compatible with a CSteamID
UserData networkHost; // set this to the host's UserData/ID

Authentication.GetAuthSessionTicket(networkHost, (TicketResponse, IOError) =>
{
    if(!IOError && TicketResponse.Result == EResult.k_EResultOK)
    {
        // Send TicketResponse.Data to your networkHost to use
    }
});
```

For Web Auth Tickets its similar but we use a string as the identity

```csharp
Authentication.GetWebAuthSessionTicket("discord", (TicketResponse, IOError) =>
{
    if(!IOError && TicketResponse.Result == EResult.k_EResultOK)
    {
        // Send TicketResponse.Data to your networkHost to use
    }
});
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Keep in mind that the Game Server and User versions are different. So if you are doing this from a Dedicated server that has initialised Steam Game Server ... then use the Steam Game Server version.&#x20;

In most cases, e.g., when running from a client build or Listen Server, you would use the User versions.

<figure><img src="../.gitbook/assets/image (360).png" alt=""><figcaption></figcaption></figure>

Note that the Web Auth Session Ticket request is asynchronous, while the standard request is not.

## C++

```cpp
TArray<uint8> buffer;
buffer.SetNumUninitialized(1024);
uint32 BytesWritten = 0;
SteamNetworkingIdentity Id{};
Id.m_eType = ESteamNetworkingIdentityType::k_ESteamNetworkingIdentityType_SteamID;
Id.SetSteamID(forSteamId);

HAuthTicket handle = SteamUser()->GetAuthSessionTicket(buffer.GetData(), 1024, &BytesWritten, &Id);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// A temp buffer to hold the max value
var array = new byte[1024];
// Will tell us the actual length
uint m_pcbTicket;
// Retain the handle for later use
var Handle = SteamUser.GetAuthSessionTicket(array, 1024, out m_pcbTicket, ref forIdentity);
// Trim the array to match the actual size
Array.Resize(ref array, (int)m_pcbTicket);
```
{% endtab %}
{% endtabs %}

### Begin Session

When you receive a ticket from a user, you use it by calling **Begin Auth Session**. This function first checks the ticket’s structure for validity. If the structure is valid, Steam processes the ticket on the backend, performs authentication, and returns the result to you.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Authentication modular component to work with Authentication in your game.&#x20;

<figure><img src="../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

Add the General Events and Sessions settings.

<figure><img src="../.gitbook/assets/image (447).png" alt=""><figcaption></figcaption></figure>

Use the Accepted Responses to indicate which response values should result in a successful authentication session. The only "pure" accept is "OK" however you may wish to allow "non-secure" servers in which case you might also add VAC Banned and VAC Check Timed Out

<figure><img src="../.gitbook/assets/image (443).png" alt=""><figcaption></figcaption></figure>

To call Sessions you should have your programmer add an event so you know when your server or host receives the ticket.

Example:

```csharp
public UnityEvent<ulong, byte[]> AuthenticationProcessor;
```

<figure><img src="../.gitbook/assets/image (444).png" alt=""><figcaption></figcaption></figure>

You can then link the BeginSession call to that event as shown above. You can use the following Events on the General Events feature to handle each of the possible Authentication cases.

<figure><img src="../.gitbook/assets/image (445).png" alt=""><figcaption></figcaption></figure>

* Invalid Ticket Received\
  This occurs when the ticket provided is malformed or otherwise structurally invalid.
* Invalid Session Requested\
  This occurs when the response from Steam for your Begin Session request is not defined in your Accepted Responses.
* Session Started\
  This occurs when the respons from Steam for your Begin Session request is defined in your Accepted Responses.

## C\#

```csharp
byte[] Data;
UserData UserItsFrom;

var RequestResult = Authentication.BeginAuthSession(Data, UserItsFrom, Session =>
{
    // This only runs if the RequestResult was okay
    // Session.User = who this session is with
    // Session.GameOwner = who owns the App they are playing on
    //                     this can be different than user if they are 
    //                     barrowing the game such as Family Sharing
    // Session.Data = this is the ticket data that was validated
    // Session.Response = this is an enumerator that tells you the status of
    //                    the request
    // Session.Barrowed = the game is barrowed e.g. User and GameOnwer dont match
    
    // Here is an example of testing the Response
    switch(Session.Response)
    {
        case EAuthSessionResponse.k_EAuthSessionResponseOK:
            // Steam has verified the user is online, 
            // the ticket is valid and ticket has not been reused.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseUserNotConnectedToSteam:
            // The user in question is not connected to steam.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseNoLicenseOrExpired:
            // The license has expired.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseVACBanned:
            // The user is VAC banned for this game.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseLoggedInElseWhere:
            // The user account has logged in elsewhere and 
            // the session containing the game instance has been disconnected.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseVACCheckTimedOut:
            // VAC has been unable to perform anti-cheat checks on this user.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketCanceled:
            // The ticket has been canceled by the issuer.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketInvalidAlreadyUsed:
            // This ticket has already been used, it is not valid.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketInvalid:
            // This ticket is not from a user instance currently connected to steam.
            break;
        case EAuthSessionResponse.k_EAuthSessionResponsePublisherIssuedBan:
            // The user is banned for this game. 
            // The ban came via the web api and not VAC
            break;
        case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketNetworkIdentityFailure:
            // The network identity in the ticket does not match 
            // the server authenticating the ticket
            break;
    }
});

// Before the callback runs, this code will run and tell us if the structure
// of the ticket provided is valid and matches the user and app
if(RequestResult != EBeginAuthSessionResult.k_EBeginAuthSessionResultOK)
{
    // If it is not "OK" then the callback will never run
    // The RequestResult tells you what is not OK about it
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Be aware of the Client vs Steam Game Server versions

<figure><img src="../.gitbook/assets/image (361).png" alt=""><figcaption></figcaption></figure>

## C++

In the example below, we are assuming your input `Ticket` came in as a TArray\<uint8> so we need to convert that to a traditional uint8 array for Steam.

```cpp
USteamToolsSubsystem* Subsystem = GEngine->GetWorld()->GetGameInstance()->GetSubsystem<USteamToolsSubsystem>();
FBeginAuthSessionCallbackDelegate callback;
callback.BindUFunction(this, FName("SteamCallback"));

Subsystem->BeginAuthRequests.Add(Request.User, callback);

int32 TicketLength = Ticket.Num();
const uint8* TicketData = Ticket.GetData();

EBeginAuthSessionResult result = SteamUser()->BeginAuthSession(TicketData, TicketLength, INT64_TO_STEAMID(Request.User));
```

We are also using Heathen's Steam Tools Subsystem to handle the callback. In this case, the input function is expected to take the form of:

```cpp
void UYourClass::SteamCallback(const int64 User, const int64 Owner, const UEAuthSessionResponse Response)
{
    // Do Work
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// Register the callback somewhere permanent if you haven't already
m_ValidateAuthSessionTicketResponse = Callback<ValidateAuthTicketResponse_t>.Create(HandleValidateAuthTicketResponse);

// To begin the session
byte[] authTicket; // This would be passed in by the user you're authenticating
var Result = SteamUser.BeginAuthSession(authTicket, authTicket.Length, user);

// The handler for your callback will take the form of
private void HandleValidateAuthTicketResponse(ValidateAuthTicketResponse_t arg0)
{
    if (arg0.m_eAuthSessionResponse != EAuthSessionResponse.k_EAuthSessionResponseOK)
        ;// Something is wrong with the ticket, the session response will say what
}
```
{% endtab %}
{% endtabs %}

### End Session

When you are done playing with a user or otherwise wish to end the authenticated session with them, you need to call End Session on that user.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Authentication modular component to work with Authentication in your game.&#x20;

<figure><img src="../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

Add the General Events and Sessions settings.

<figure><img src="../.gitbook/assets/image (447).png" alt=""><figcaption></figcaption></figure>

You can use the Sessions feature to call End or EndAll to end sessions with a specific user or all users.

<figure><img src="../.gitbook/assets/image (448).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
End and End All does —NOT— affect your network, it is up to you to end/close connections via your HLAPI of choice.
{% endhint %}

## C\#

```csharp
// End for a user
Authentication.EndAuthSession(TheUser);

// End for all users
Authentication.EndAllSessions();
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Be aware of the Client vs Steam Game Server versions

<figure><img src="../.gitbook/assets/image (363).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// For client builds
SteamUser()->EndAuthSession(SteamId);
// For dedicated server builds
SteamGameServer()->EndAuthSession(SteamId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// For client builds
SteamUser.EndAuthSession(User);
// For dedicated server builds
SteamGameServer.EndAuthSession(User);
```
{% endtab %}
{% endtabs %}
