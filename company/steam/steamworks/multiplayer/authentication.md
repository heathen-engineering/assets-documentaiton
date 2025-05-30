---
description: >-
  Understanding Steam Authentication, when and why to use it ... and when and
  why not to.
---

# 🧑‍⚖️ Authentication

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% embed url="https://partner.steamgames.com/doc/features/auth" %}

{% hint style="info" %}
The above link and repeated below so you can find it:\
[https://partner.steamgames.com/doc/features/auth](https://partner.steamgames.com/doc/features/auth)\
\
Is highly important, that you should fully read Valve's own documentation around Steam Authentication to fully understand it. Some of the information will be summarized herein and notes on the tools and systems Heathen has created around Steam Authentication.&#x20;
{% endhint %}

## Unity

Heathen's Authentication API handles both Client and Server authentication and manages the ticket and session data generated for you.

{% content-ref url="../../../../old-toolkit-for-steamworks/unity/api-extensions/authentication.md" %}
[authentication.md](../../../../old-toolkit-for-steamworks/unity/api-extensions/authentication.md)
{% endcontent-ref %}

You will notice that unlike other APIs there is no Client or Server or Web version. Because the Steam API endpoints have the same requirements and signatures for all targets we can select the correct endpoint for you based on the build type.

That is for a client or "normal" build we will use the Client endpoints and for a server build or "headless" build we will use the Server endpoints.

### Generate Ticket

[Get Auth Session Ticket](../../../../old-toolkit-for-steamworks/unity/api-extensions/authentication.md#getauthsessionticket)

```csharp
Authentication.GetAuthSessionTicket(identity, (ticket, IOError) =>
{
    if(!IOError)
    {
        SendToServer(UserData.Me, ticket.data);
    }
});
```

This ticket contains a bit of information but the important part is the data represented as a byte\[]

This is the data that should be sent to whoever or whatever it is that will be authenticating this subject. So send it to your game server or your peer if you doing peer-to-peer authentication ... and yes peer-to-peer authentication can be done.

### Send Ticket

How exactly you send the ticket is between you and your networking tool or your lobby system.&#x20;

{% hint style="success" %}
For example in a Peer to Peer game where you are using Steam Inventory items, you may want to validate that all members of a lobby do own the items they claim to own. You can use Steam Authentication for this by starting an authentication session between each user and sending a serialized copy of the inventory items. Steam clients can then validate that yes they are owned and who they are owned by.
{% endhint %}

In any case, you will need to send 2 bits of information being&#x20;

1. The user ID of the user who generated the ticket
2. The byte\[] e.g. "Ticket Data" that was generated

{% hint style="info" %}
Each ticket can be used exactly once and does expire after some time. So for example, if you want to have every peer in a P2P game authenticate every other peer then every player will need to generate 1 ticket for every other player and will need to validate 1 ticket from every other player.
{% endhint %}

### Begin Auth Session

[Begin Auth Session](../../../../old-toolkit-for-steamworks/unity/api-extensions/authentication.md#beginauthsession)

```csharp
void AuthenticatUser(byte[] ticket, UserData user)
{
    var responce = Authentication.BeginAuthSession(ticket, user, result =>
    {
        switch(result.responce)
        {
            case EAuthSessionResponse.k_EAuthSessionResponseOK:
                //All is well
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseUserNotConnectedToSteam:
                //This user is not connected to Steam
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseNoLicenseOrExpired:
                //This user is not licensed for this game
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseVACBanned:
                //This user is VAC banned for this app
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseLoggedInElseWhere:
                //This session is logged elsewhere
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseVACCheckTimedOut:
                //This VAC Check is timed out, may be fine, may not
            break;
            case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketCanceled:
                //This Tickedt cancelled by the owner
            break;
            case EAuthSessionResponse.k_EAuthSessionResponsePublisherIssuedBan:
                //This publisher issued ban
            break;
            
            case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketInvalidAlreadyUsed:
                //This Ticket invalid / already used
            break;
            
            case EAuthSessionResponse.k_EAuthSessionResponseAuthTicketInvalid:
                //This Ticket invalid
            break;
        }
    });
    
    switch(responce)
    {
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultOK:
            //Send correctly, wait for callback
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultInvalidTicket:
            //Invalid ticket will get no response
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultDuplicateRequest:
            //Duplicate requests will get no response
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultInvalidVersion:
            //Invalid version will get no response
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultGameMismatch:
            //Game mismatch will get no response
        break;
        case EBeginAuthSessionResult.k_EBeginAuthSessionResultExpiredTicket:
            //Expired ticket, will get no response
        break;
    }
}
```

This simply takes in the ticket and user ID that generated it and asks Steam API to validate it. The results of this call will tell you whether or not it's valid and will give you details about the authenticated user such as whether or not they are VAC banned, how exactly they own a license to the App they are authenticating from and for, etc.

Having authenticated a user allows for a few additional features. For example, a Steam Game Server identifies the users playing on it by what Auth Sessions are active. That is when you Begin Auth Session for a user you are telling Valve that said user is playing on that server, when you end the session you are telling Valve that the user is no longer playing.

### End Auth Session

[End Auth Session](../../../../old-toolkit-for-steamworks/unity/api-extensions/authentication.md#endauthsession)

```csharp
void UserLoggedOff(UserData user)
{
    Authentication.EndAuthSession(user);
}
```

When a game session is done you should notify Valve that the session is over by ending the auth session.

### Verify Inventory

A common use for authentication sessions is to validate that a given user owns specific inventory items. This can only be done once an Authentication Session has been started with that user. This can be done on Client to Client or Client to Server.

You can either serialize the local user's whole inventory (rare)

[Serialize All Item Results](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#serializeallitemresults)

or you can serialize specific items (more common)

[Serialize Item Results By ID](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#serializeitemresultsbyid)

In either case, the result is a byte\[] of data that represents the inventory state at the time of serialization, who that inventory was read from and when it was read.

```csharp
//Assume that instanceIds is the collection of items you want to send
SteamItemInstnaceID_t[] instanceIds;

Inventory.Client.SerializeItemResultsByID(instanceIds, data =>
{
    SendDataToRequestingParty(UserData.Me, data);
});
```

Once you have this byte\[] you should send it to who or whatever it is that needs to validate ownership of the items.

The specifics of sending the data are between you and your networking tools, the important thing is that you are sending 2 bits of data

1. The user ID that generated the serialized inventory data
2. The data itself

When your peer or server receives this data they can read its details

[Deserialize Result](../../../../old-toolkit-for-steamworks/unity/api-extensions/inventory.client.md#destroyresult)

```csharp
void ValidateInventory(UserData user, byte[] data)
{
    Inventory.Client.DeserializeResult(user, data, responce =>
    {
        if(responce.result == EResult.k_EResultOK)
        {
            Debug.Log(user.Nickname + " owns these " + items.length + " items");
        }
        else if(responce.result == EResult.k_EResultExpired)
        {
            Debug.LogWarning(user.Nickname + " owns them, but this data is old.");
        }
    });
}
```

## Unreal

### Generate Ticket

The [Get Auth Session Ticket](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/get-auth-session-ticket.md) node will return an [Auth Ticket Data](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/types/auth-ticket-data.md) object containing the handle and byte array of the ticket. The "For Steam ID" value should be set to the Steam ID of the User or Server that will be using the ticket in the Begin Auth Session process.

<figure><img src="../../../../.gitbook/assets/image (24).png" alt=""><figcaption><p>Client version of the node</p></figcaption></figure>

If you are sending the ticket to a system using Steam Web API then you need to use the [Get Web Auth Session Ticket](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/get-auth-ticket-for-web-api.md) in its place and the identity you pass in should match the identity used by that web app.

### Send Ticket

How you send the ticket to the user, server or web API using it is up to you. You can use a Remote Procedure Call, sync it over a data field, pass it as part of a Lobby Chat Message, etc. The important thing is that the subject who receives the ticket data knows the Steam ID of the user the Ticekt is supposedly for as they will need that information to "Begin Auth Session"

### Begin Auth Session

Note the Client and Server variants of the [Begin Auth Session](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/begin-auth-session.md) node, only a[ Steam Game Server](game-server-browser/) should use the Server version and only a Client should use the Client version.

The Steam ID field is the ID of the entity this ticket is believed to be from

<figure><img src="../../../../.gitbook/assets/image (19) (1).png" alt=""><figcaption><p>For use by clients</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (268).png" alt=""><figcaption><p>For use by Steam Game Servers</p></figcaption></figure>

### End Auth Session

Note the Client and Server variants of the [End Auth Session](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/end-auth-session.md) node, only a[ Steam Game Server](game-server-browser/) should use the Server version and only a Client should use the Client version.

The Steam ID field is the ID of the entity to end the session relationship with.

<figure><img src="../../../../.gitbook/assets/image (21) (1).png" alt=""><figcaption><p>For use by clients</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (273).png" alt=""><figcaption><p>For use by Steam Game Servers</p></figcaption></figure>

### Verify Inventory

See the [Serialize Result](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/serialize-result.md) and [Deserialize Result](../../../../old-toolkit-for-steamworks/unreal/blueprint-nodes/functions/deserialize-result.md) articles for details on the nodes and usage for verifying inventory ownership via the Steam Authentication system.
