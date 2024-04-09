---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Parties.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using Parties = HeathenEngineering.SteamworksIntegration.API.Parties.Client;
```

```csharp
public static class Parties.Client
```

### What can it do?

You can use this system as a matchmaking solution where in your user can scan for available beacons to join and can create and publish beacons that others can view and join.

You can attach metadata to a beacon similar to the metadata concept with [Steam Lobby](../../../company/steam/steamworks/multiplayer/matchmaking-tools.md) based matchmaking. You can use the party system along side other forms of matchmaking manually updating the available "slots" a beacon is advertising.



Its always wise to review the source documentation for any API:

From Steam's documentation:&#x20;

{% embed url="https://partner.steamgames.com/doc/api/isteamparties" %}

> This API can be used to selectively advertise your multiplayer game session in a Steam chat room group. Tell Steam the number of player spots that are available for your party, and a join-game string, and it will show a beacon in the selected group and allow that many users to “follow” the beacon to your party. Adjust the number of open slots if other players join through alternate matchmaking methods.\
> \
> For example, you can use ISteamParties in conjunction with a private lobby. Create a private lobby, and then use [ISteamParties::CreateBeacon](https://partner.steamgames.com/doc/api/ISteamParties#CreateBeacon) to create a party "beacon" for the number of players desired. The game connect string should indicate the ID of the private lobby.\
> \
> The beacon will appear in Steam in the specified location (e.g. a Chat Room Group), and also via the in-game ISteamParties API as described below. Steam creates "reservation" slots for the number of desired players. Whenever a user follows the beacon, Steam will hold a reservation slot for them and launch the game using the given connect string.\
> \
> The game session that created the beacon will be notified of this reservation, so the game can display the appropriate "User \<username> is joining your party" or some other indicator. Once the user joins successfully, the game session should call [ISteamParties::OnReservationCompleted](https://partner.steamgames.com/doc/api/ISteamParties#OnReservationCompleted) to tell Steam that the user successfully joined (otherwise, Steam will eventually timeout their reservation and re-open the slot).\
> \
> When all of the beacon slots are occupied - either by reservations for users still launching the game, or completed slots for users in the party - Steam will hide and disable the beacon.\
> \
> To cancel the beacon - for instance when the party is full and the game begins - call [ISteamParties::DestroyBeacon](https://partner.steamgames.com/doc/api/ISteamParties#DestroyBeacon).\
> \
> The client side of this operation - seeing and following beacons - can also be managed by your game. Using [ISteamParties::GetNumActiveBeacons](https://partner.steamgames.com/doc/api/ISteamParties#GetNumActiveBeacons) and [ISteamParties::GetBeaconDetails](https://partner.steamgames.com/doc/api/ISteamParties#GetBeaconDetails), your game can get a list of beacons from other users that are currently active in locations relevant to the current user. If the user desires, call [ISteamParties::JoinParty](https://partner.steamgames.com/doc/api/ISteamParties#JoinParty) to "follow" one of those beacons.

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/party-beacon-details" %}

## Events

### Reservation Notificaiton Callback

```csharp
public static ReservationNotificationCallbackEvent EventReservationNotificationCallback
```

Called when a user joins your party. You should call the OnReservationCompleted method to notify Steam that the user has joined successfully.

The handler for this event would look like this

```csharp
public void HandleEvent(ReservationNotificationCallback_t arg)
{
    //Do Work
}
```

{% hint style="info" %}
The Steamworks Complete system tracks these reservations for you in the reservations array.&#x20;

\
When you call complete on a reservation we remove the reservation from the tracked array.
{% endhint %}

### Active Beacons Updated

```csharp
public static ActiveBeaconsUpdatedEvent EventActiveBeaconsUpdated
```

Notification that the list of active beacons visible to the current user has changed.

The handler for this event would look like this

```csharp
public void HandleEvent(ActiveBeaconsUpdated_t arg)
{
    //Do Work
}
```

You can get a list of the beacons this user can see by calling [List Beacons](parties.client.md#list-beacons)

### Available Beacon Locations Updated

```csharp
public static AvailableBeaconLocationsUpdatedEvent EventAvailableBeaconLocationsUpdated
```

Notification that the list of available locations for the posting of a beacon has been updated.

The handler for this event would look like this.

```csharp
public void HandleEvent(AvailableBeaconLocationsUpdated_t arg)
{
    //Do Work
}
```

You can get a list of available beacon locations by calling [Get Available Beacon Locations](parties.client.md#get-available-beacon-locations)

## Fields and Attributes

### MyBeacons

```csharp
public static PartyBeaconID_t[] MyBeacons => get;
```

An array of beacons created by this user in this session that have not yet been destroyed.

### Reservations

```csharp
public static ReservationNotificationCallback_t[] Reservations
```

The list of reservations that you have been notified about but that have not yet been completed.

## Methods

### GetAvailableBeaconLocations

```csharp
public static SteamPartyBeaconLocation_t[] GetAvailableBeaconLocations()
```

Gets a list of the available beacon locations, these are the locations where you can create a beacon for users to join.

You would generally use this in conjunction with Create Beacon to create a new beacon.

### CreateBeacon

```csharp
public static void CreateBeacon(uint openSlots, 
                ref SteamPartyBeaconLocation_t location, 
                string connectionString, 
                string metadata, 
                Action<CreateBeaconCallback_t, bool> callback)
```

Creates a beacon at the location indicated.

* openSlots\
  This is how many slots / people should be advertised as available on this beacon.
* location\
  This is the location you wish to create this beacon on
* connectionString\
  This is the connection string associated with the beacon and will be used to launch the game when a user follows this beacon.
* metadata\
  This is additional data that can be added to a beacon ... you can fetch the metadata for a beacon by calling GetBeaconDetails
* callback\
  This is an action i.e. a method pointer that will be invoked when the create operation is completed

The callback should have the following form

```csharp
public void HandleCallback(CreateBeaconCallback_t arg, bool IOError)
{
    //Do Work
}
```

### OnReservationCompleted

```csharp
public static void OnReservationCompleted(PartyBeaconID_t beacon, CSteamID user)
```

```csharp
public static bool OnReservationCompleted(UserData user)
```

{% hint style="info" %}
When using the overload that only takes a UserData value the method will return \
True when a matching beacon was found and updated\
False when no matching beacon was found for this user and no action was taken
{% endhint %}

This should be called when a user joins from a beacon to notify Steam that the reservation has been completed.

The Steamworks Complete system will track all open reservations so its possible to complete a reservation knowing only the user's ID. It is more efficient however to pass in both the beacon and user as this saves the system from needing to look up the related beacons.

### ChangeNumberOpenSlots

```csharp
public static void ChangeNumOpenSlots(PartyBeaconID_t beacon, 
        uint openSlots, 
        Action<ChangeNumOpenSlotsCallback_t, bool> callback)
```

This should be used if a user joins your session through other matchmaking solutions such as a direct steam friend invite or similar. This simply updates the number of open slots remaining. Note that if a user joins via a beacon i.e. you get a reservation and complete it then Steam will update the open slots accordingly.

* beacon\
  The beacon to be updated
* openSlots\
  The remaining open slots
* callback\
  An action/method to be invoked when completed

The callback for this method should look like this

```csharp
public void HandleCallback(ChangeNumOpenSlotsCallback_t arg, bool IOError)
{
    //Do Work
}
```

### DestroyBeacon

```csharp
public static bool DestroyBeacon(PartyBeaconID_t beacon)
```

This will destroy the beacon and stop showing it. Any users already in flight may still arrive and expect to join.

### GetBeacons

```csharp
public static PartyBeaconID_t[] GetBeacons()
```

Gets the array of beacons created by other users that this user can see.

### GetBeaconDetails

```csharp
public static PartyBeaconDetails? GetBeaconDetails(PartyBeaconID_t beacon)
```

Returns the details of a specific beacon if any was found

### JoinParty

```csharp
public static void JoinParty(PartyBeaconID_t beacon, 
        Action<JoinPartyCallback_t, bool> callback)
```

Used when the user is in game and has a beacon they would like to join. Call this and Steam will makes the necessary reservation and pull back the connection data in the resulting callback.

* beacon\
  The beacon to join
* callback\
  An action / method pointer to call when the process is complete and the reservation made

The callback for this method should look like this

```csharp
public void HandleCallback(JoinPartyCallback_t arg, bool IOError)
{
    //Do Work
}
```

### GetBeaconLocationData

```csharp
public static bool GetBeaconLocationData(SteamPartyBeaconLocation_t location, 
        ESteamPartyBeaconLocationData data, 
        out string result)
```

Query general metadata for the given beacon location. For instance the Name, or the URL for an icon if the location type supports icons (for example, the icon for a Steam Chat Room Group).



## How To

### Get Available Beacon Locations

Get the list of locations in which you can post a party beacon.

```csharp
var results = Parties.GetAvailableBeaconLocations();
```

### Create Beacon

Create a beacon. You can only create one beacon at a time. Steam will display the beacon in the specified location, and let up to unOpenSlots users "follow" the beacon to your party.

```csharp
Parties.ent.CreateBeacon(
        openSlots, 
        ref location, 
        connectionString, 
        metadata, 
        callback);
```

{% hint style="info" %}
The system will automatically track your created beacons in the [MyBeacons](parties.client.md#mybeacons) array
{% endhint %}

The connectionString should be the data you want the user to use to connect to your party. When a user joins your party from outside the game this will be passed in as Valve launches your game. If the user joins form within the game it will be provided to them in the JoinParty callback.

Your game needs to handle this connectionString and take necessary actions. For example if this connectionString is the CSteamID of a P2P connection they should join then your game should navigate to the proper scene and then connect to that CSteamID. What this is will depend very much on how your game defines a party i.e. is it a game server, a P2P host, a lobby, etc.

### Complete Reservation

When a user follows your beacon, Steam will reserve one of the open party slots for them, and send your game a ReservationNotificationCallback\_t callback. When that user joins your party, call OnReservationCompleted to notify Steam that the user has joined successfully.

```csharp
API.Parties.Client.OnReservationCompleted(beacon, user);
```

{% hint style="info" %}
The system will automatically track all pending reservations for you in the [Reservations ](parties.client.md#reservations)array.
{% endhint %}

### Change Slot Count

If a user joins your party through other matchmaking (perhaps a direct Steam friend, or your own matchmaking system), your game should reduce the number of open slots that Steam is managing through the party beacon. For example, if you created a beacon with five slots, and Steam sent you two ReservationNotificationCallback\_t callbacks, and then a third user joined directly, you would want to call ChangeNumOpenSlots with a value of 2 for unOpenSlots. That value represents the total number of new users that you would like Steam to send to your party.

```csharp
API.Parties.Client.ChangeNumOpenSlots(beacon, slots, callback);
```

### Destroy Beacon

Call this method to destroy the Steam party beacon. This will immediately cause Steam to stop showing the beacon in the target location. Note that any users currently in-flight may still arrive at your party expecting to join.

```csharp
API.Parties.Client.DestroyBeacon(beacon);
```

### List Beacons

Get the collection of active beacons visible to the current user.

```csharp
var beacons = API.Parties.Client.GetBeacons();
```

### Get Beacon Details

Get details about the specified beacon.

```csharp
var details = API.Parties.Client.GetBeaconDetails(beacon);
```

### Join Party

When the user indicates they wish to join the party advertised by a given beacon, call this method. On success, Steam will reserve a slot for this user in the party and return the necessary "join game" string to use to complete the connection.

```csharp
API.Parties.Client.JoinParty(beacon, callback);
```

### Get Beacon Location Data

Query general metadata for the given beacon location. For instance the Name, or the URL for an icon if the location type supports icons (for example, the icon for a Steam Chat Room Group).

```csharp
API.Parties.Client.GetBeaconLocationData(location, data, result);
```

