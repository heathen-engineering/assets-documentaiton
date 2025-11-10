# Party

Steam Parties is a feature provided by Steam that allows players to form temporary groups (called _parties_) through the Steam UI, which can then join multiplayer games together. Unlike Steam Lobbies, which manage peer-to-peer connections directly, Steam Parties is a _party discovery_ and _reservation_ system meant to complement your game’s existing networking solution.

Steam Parties handles the _social layer_—showing party beacons in the Steam Overlay, allowing players to express interest in joining, and coordinating "join game" actions.

{% embed url="https://partner.steamgames.com/doc/api/isteamparties" %}

### When to Use (or Not Use) Steam Parties

**Use Steam Parties if:**

* Your game supports group play, and you want to make it easy for players to invite friends before they enter the game.
* You want to allow players to advertise open party slots via Steam’s built-in UI (overlay, friends list, etc.).
* You want to handle party joining via a clean "join game" string (e.g., Steam Lobby ID, IP:Port, etc.) that your game can process.

**Do not use Steam Parties if:**

* You already use Steam Lobbies exclusively for player discovery and matchmaking.
* Your game requires complex matchmaking, ranked queues, or large-scale persistent sessions.
* You don’t want players joining each other from the Steam UI (e.g., single-player or private game setups).

Steam Parties is not a networking layer. It doesn’t manage connections, replication, or matchmaking logic. It only provides a way for users to find and join a party from Steam’s social interface.

### Core Structure of Steam Parties

Steam Parties revolves around these key components:

* **Beacon Locations**: Places where a party can be advertised (e.g., a region, game mode, or custom area). The game provides these when requested by Steam.
* **Party Beacons**: Advertisements created by a player to indicate they are hosting a party and looking for others to join. These beacons appear in the Steam Overlay.
* **Join Requests**: When a user clicks to join a party via a beacon, Steam notifies the host. The host can accept and provide a join string (like a server IP or lobby ID).
* **Join Game Strings**: These are opaque connection details returned to Steam after a successful join. Your game uses this string to connect the joining user to the session.

Steam Parties is designed to be a lightweight, session-based tool that works in tandem with your game's connection system.

## Examples

### Create Beacon

When using Steam Parties, Steam provides you with a list of available beacon locations. These locations indicate where your party beacon can be advertised within Steam’s ecosystem. Currently, Steam defines these locations as chat groups. For example, you might see your own chat group during a stream or a specific "Clan" group that your game supports.

When your game queries for available beacon locations, it receives a list of structures that tell you exactly where your party beacon can be displayed. You then select the most appropriate location for your session, and Steam will advertise your beacon within that specific chat context.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not Applicable

## C\#

```csharp
public void CreateBeacon()
{
    // Make sure Steam and the Parties system are initialized.
    // Retrieve the list of available beacon locations.
    SteamPartyBeaconLocation_t[] availableLocations = Parties.Client.GetAvailableBeaconLocations();
    if (availableLocations == null || availableLocations.Length == 0)
    {
        Debug.LogWarning("No available beacon locations found.");
        return;
    }

    // Select a beacon location (using the first one for this example).
    SteamPartyBeaconLocation_t selectedLocation = availableLocations[0];

    // Set up the join string which provides connection details to joining players.
    string joinString = "JoinGameSessionToken123";

    // Set metadata (for example, game mode or map details).
    string metadata = "GameMode=Deathmatch;Map=Arena";

    // Set the number of open slots (e.g., if the host takes one slot and three open slots remain).
    uint openSlots = 3;

    // Create a beacon using your custom API.
    Parties.Client.CreateBeacon(openSlots, ref selectedLocation, joinString, metadata, OnCreateBeacon);
}
```

The handler would look like this

```csharp
private void OnCreateBeacon(CreateBeaconCallback_t result, bool ioFailure)
{
    if (ioFailure)
    {
        Debug.LogError("I/O Failure occurred while creating beacon.");
        return;
    }

    // Check if the creation was successful.
    if (result.m_eResult == EResult.k_EResultOK)
    {
        Debug.Log("Beacon created successfully. Beacon ID: " + result.m_ulBeaconID);
    }
    else
    {
        Debug.LogError("Failed to create beacon. Steam error: " + result.m_eResult);
    }
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Not available in the current versions of Unreal.
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// Retrieve the number of available beacon locations.
SteamParties.GetNumAvailableBeaconLocations(out uint numLocations);
if (numLocations == 0)
{
    Debug.LogWarning("No available beacon locations found.");
    return;
}

// Create an array to hold the available locations.
SteamPartyBeaconLocation_t[] availableLocations = new SteamPartyBeaconLocation_t[numLocations];
SteamParties.GetAvailableBeaconLocations(availableLocations, numLocations);

// Select a beacon location (using the first one for this example).
SteamPartyBeaconLocation_t selectedLocation = availableLocations[0];

// Set up the join string which provides connection details to joining players.
string joinString = "JoinGameSessionToken123";

// Set metadata (for example, game mode or map details).
string metadata = "GameMode=Deathmatch;Map=Arena";

// Set the number of open slots (e.g., if the host takes one slot and three open slots remain).
uint openSlots = 3;

// Create the beacon using Steamworks.NET native API.
var beaconHandle = SteamParties.CreateBeacon(openSlots, ref selectedLocation, joinString, metadata);

// Set up the callback using CallResult.
if (createBeaconCallResult == null)
    createBeaconCallResult = CallResult<CreateBeaconCallback_t>.Create();

createBeaconCallResult.Set(beaconHandle, OnCreateBeacon);
```

Your callback would look similar to this

```csharp
private void OnCreateBeacon(CreateBeaconCallback_t result, bool ioFailure)
{
    if (ioFailure)
    {
        Debug.LogError("I/O Failure occurred while creating beacon.");
        return;
    }

    if (result.m_eResult == EResult.k_EResultOK)
    {
        Debug.Log("Beacon created successfully. Beacon ID: " + result.m_ulBeaconID);
    }
    else
    {
        Debug.LogError("Failed to create beacon. Steam error: " + result.m_eResult);
    }
}
```
{% endtab %}
{% endtabs %}

### Get Available Beacons

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not Applicable

## C\#

```csharp
// Get the list of active beacon IDs.
PartyBeaconID_t[] beaconIDs = Parties.Client.GetBeacons();
if (beaconIDs == null || beaconIDs.Length == 0)
{
    Debug.Log("No active beacons found.");
    return;
}

Debug.Log("Active beacons count: " + beaconIDs.Length);

// Iterate over each beacon ID.
foreach (PartyBeaconID_t beaconId in beaconIDs)
{
    // Optionally, get details about the beacon.
    var beaconDetails = Parties.Client.GetBeaconDetails(beaconId);
    if (beaconDetails.HasValue)
    {
        Debug.Log($"BeaconID: {beaconId} | Owner: {beaconDetails.Value.owner} | Metadata: {beaconDetails.Value.metadata}");
    }
    else
    {
        Debug.Log($"BeaconID: {beaconId} - No details available.");
    }
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Not available in the current versions of Unreal.
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// Get the count of active beacons.
uint beaconCount = SteamParties.GetNumActiveBeacons();
if (beaconCount == 0)
{
    Debug.Log("No active beacons found.");
    return;
}

Debug.Log("Active beacons count: " + beaconCount);

// Loop through the beacons using their index.
for (uint i = 0; i < beaconCount; i++)
{
    // Retrieve the beacon ID using its index.
    PartyBeaconID_t beaconID = SteamParties.GetBeaconByIndex(i);

    // Retrieve beacon details: owner, location, and metadata.
    if (SteamParties.GetBeaconDetails(beaconID, out CSteamID owner, out SteamPartyBeaconLocation_t location, out string metadata, 8193))
    {
        Debug.Log($"BeaconID: {beaconID} | Owner: {owner} | Metadata: {metadata}");
    }
    else
    {
        Debug.Log($"BeaconID: {beaconID} - No details available.");
    }
}
```
{% endtab %}
{% endtabs %}

### Join a Party

When a user clicks on a beacon in a Steam Chat, it’s known that the host will receive a notification via the Reservation Notification Callback—this part is documented by Steam. This callback informs the creator of the beacon that someone has shown interest by clicking it. Once the callback fires, it’s up to the host’s game logic to process and respond to the join attempt.

The behavior after that click is not documented by Valve, and we haven’t had the opportunity to test it in depth. However, the common consensus is that the same workflow used for Join Game is likely triggered. In other words, if the user is not already playing the game, Steam will launch the game while passing the beacon ID through the command line. If the game is already running, Steam should raise a Rich Presence Join Requested callback. Once the player successfully connects, it’s then the host’s responsibility to call OnReservationCompleted to update the number of open slots for the beacon. If this isn’t done in time, the reserved slot may be released, though the precise timeout is not documented.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not Applicable

## C\#

You can review [Friends Invite to Game](user.md#invite-to-game) to understand how the player who clicks a beacon will be notified in-game what to connect to. That is, we believe (it's not documented) that when a user clicks a beacon that it works the same as clicking Join Game from the friends list or being invited to a game directly.

```csharp
// The beacon ID passed in on the connect command line 
// or the connection string in Rich Presence Join Requested
PartyBeaconID_t beacon = new PartyBeaconID_t(123456789);
Parties.Client.JoinParty(beacon, HandleJoinParty);
```

The HandleJoinParty might look like this

```csharp
private void HandleJoinParty(JoinPartyCallback_t Callback, bool IOError)
{
    // Callback.m_rgchConnectString: the connection string to connect to
    // Callback.m_SteamIDBeaconOwner, who you're looking to connect to
    // Callback.m_eResult the EResult of the request to join ... should be OK
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Not available in the current versions of Unreal.
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Destroy Beacons

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not applicable

## C\#

```csharp
// Given a beacon such as
PartyBeaconID_t beacon = new PartyBeaconID_t(123456789);

// Then
Parties.Client.DestroyBeacon(beacon);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Not available in the current versions of Unreal.
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
// Given a beacon such as
PartyBeaconID_t beacon = new PartyBeaconID_t(123456789);

// Then
SteamParties.DestroyBeacon(beacon);
```
{% endtab %}
{% endtabs %}
