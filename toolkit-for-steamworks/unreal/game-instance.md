---
cover: ../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
---

# Game Instance

## Introduction

{% hint style="info" %}
Game Instance is a good place for global things to our game. \
Steam has quite a few global scoped "events" that we have exposed for you via the Steam Game Instance.\
This is also a good place to store the Steam ID's for the lobbies your players have joined, created, etc. See [Use](game-instance.md#use) for more details.
{% endhint %}

Steamworks requires a few system-level features to function correctly such as a constant and steady call to Run\_Callbacks, management of delegates handling system-level callbacks and management of artefacts loaded from Steam and referenced in Unreal such as images, inventory results, etc.

To handle this for you Heathen has created the Steam Game Instance class which extends Unreal's native Game Instance class. To use Steamworks you should create a new Blueprint based on Steam Game Instance or use the provided BP\_Steam\_Game\_Instance.

<figure><img src="../../.gitbook/assets/image (347).png" alt=""><figcaption></figcaption></figure>

### Callback Frequency

{% hint style="info" %}
Not applicable when using Steam Sockets as it will handle the callbacks on a background thread. This is however used if you are not initializing Online Subsystem Steam at all such as when working in the editor.
{% endhint %}

Expressed in seconds this is the time between Run Callback calls. This is an important value as it dictates how frequently messages from Valve's Steam will be invoked as callback delegates in your game. This impacts all asynchronous features of Steam which is most of them.

The system will clamp this value to be between 0.1 and 0.01 e.g. 10Htz to 100Htz the typical range being more frequently 30Htz to 60Htz

## Initialization

Initialization is smart, if the API has been initialized by another system it will go with it and will still invoke the success events.

<figure><img src="../../.gitbook/assets/image (349).png" alt=""><figcaption></figcaption></figure>

You will notice that initialization does require the use of a few nodes. The main node here is the Initialize Steam API function node. This will read the configuration you have provided from the Steam Game Instance and initialize Steam API for you. It will always initialize Steam Client API endpoints when executing on a client or listen server and will always initialise Steam Game Server API endpoints when executing on a dedicated server aka a "headless" server.

If you are building a dedicated server you will likely want to read the server configuration from some external source prior to calling this node.

The output of the node will indicate success or failure. If you are initializing for a client/listen server it may also indicate "Should Restart". This is a feature of Steam API, if the game was not launched from the Steam client then it will attempt to relaunch from the Steam client ... so if this is true you should close the game as Steam will be relaunching it from the Steam client its self.

Finally, we call a few event handlers so we can better organize our nodes.

## Events

<figure><img src="../../.gitbook/assets/image (350).png" alt=""><figcaption></figcaption></figure>

### Should Restart

This occurs in the event that the game was not launched from the Steam client. It indicates that Steam API is attempting to relaunch the game from the Steam client and thus this instance of the game should be closed.

### Failed to Initialize

This generally only happens if your user isn't logged into Steam, doesn't have Steam installed at all or doesn't own the game and thus the API can't initialize. In this case, you should generally notify the user of this issue and its common causes and then close the game gracefully.

### Bootstrapping

The Bootstrap Your Game Here is the ideal place to warm up your game systems and runs right after Steam API has successfully initialized. This is where you would enable Steam Input, find your leaderboards, load system settings, read the player's inventory and initialise any additional game systems relevant to your game.

## Use

### Game Instance Varaible

The Steam Game Instance has all of Steam's global events and you can register to them easily by adding a Steam Game Instance (or your derived class) as a variable to whatever blueprint you want to leverage the events from. In the constructor for that blueprint set the variable to Steam Game Instance casting to whatever specific type you might need.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
Every blueprint you make will have a construction function ready for you to set up. \
This is where you should set the Game Instance variable as this happens before anything else so you will know that this will always be set when this object is in scope.![](<../../.gitbook/assets/image (2) (1).png>)
{% endhint %}

Once we have our Game Instance variable created and the logic to set it in the Construction Script we can then leverage the events from the instance as you would any other Blueprint event

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### Lobby Data

Steam Lobbies are generally a key part of your game and they are relevant between scene transitions. Its generally in your interest to store data about the lobbies your player is in on the Game Instance where it will happily persist and can easily be accessed from anywhere.

#### Custom Game Instance

Create a custom game instance derived from Steam Game Instance&#x20;

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
DO NOT:\
Derive from the BP\_SteamGameInstance\
That is simply a working example of how to do this you can check for ideas on how to set up your events.
{% endhint %}

#### Lobby Variable

Create a new variable of type Integer 64 ... this is where we will store our lobby ID when a lobby is created, joined, etc.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

#### Handy Game Funcitons

Create functions that use the lobby and are specific to your game

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

These will be specific to your particular game, in this example our game has a concept of teams so we make a function to get or set the team for a player on the lobby metadata.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

This function... again specific to our game ... this is just idea food for you to get thinking ...

Our function here takes in the Steam ID of the user to who we are setting the team as well as a Gameplay Tag that represents which team they will be assigned to.

We get the Hex ID from the Steam ID ... this just makes that long number a shorter Hex string

We append \_Team to that and use the result as the "key" in our lobby data ... this will look something like `ABCD1234_Team`

We get the string name of our Team ... this might look like `State.Team.1` which we set as the "value" of the key.

The end result is we have now stored `ABCD1234_Team = State.Team.1` on our lobby as metadata ... this can then be read back by any member of the lobby at any time by simply getting the Game Instance and calling Get Team to return the Gameplay Tag that is the player's team.
