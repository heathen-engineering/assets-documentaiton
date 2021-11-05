# Parties

{% hint style="warning" %}
Coming Soon

This will be released with Patch 13 and is expected late 2021 to early 2022 as a free update to Steamworks V2
{% endhint %}

## Introduction

```csharp
public static class API.Parties
```

The whole of the parties system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Parties.Client
```

### What can it do?

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

## Events

### Reservation Notificaiton Callback

Called when a user joins your party. You should call the OnReservationCompleted method to notify Steam that the user has joined successfuly.

### Active Beacons Updated

Notification that the list of active beacons vissible to the current user has changed.

### Available Beacon Locations Updated

Notification that thhe list of available locateions for the posting of a beacon has been updated.

## How To

### Get Available Beacon Locations

Get the list of locations in which you can post a party beacon.

```csharp
var results = API.Parties.Client.GetAvailableBeaconLocations();
```

### Create Beacon

Create a beacon. You can only create one beacon at a time. Steam will display the beacon in the specified location, and let up to unOpenSlots users "follow" the beacon to your party.

```csharp
API.Parties.Client.CreateBeacon(
        openSlots, 
        ref location, 
        connectionString, 
        metadata, 
        callback);
```

### Complete Reservation

When a user follows your beacon, Steam will reserve one of the open party slots for them, and send your game a ReservationNotificationCallback\_t callback. When that user joins your party, call OnReservationCompleted to notify Steam that the user has joined successfully.

```csharp
API.Parties.Client.OnReservationCompleted(beacon, user);
```

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

