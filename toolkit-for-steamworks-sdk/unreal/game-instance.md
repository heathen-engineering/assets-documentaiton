---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
---

# Game Instance

## Introduction

Steamworks requires a few system-level features to function correctly such as a constant and steady call to Run\_Callbacks, management of delegates handling system-level callbacks and management of artefacts loaded from Steam and referenced in Unreal such as images, inventory results, etc.

To handle this for you Heathen has created the Steam Game Instance class which extends Unreal's native Game Instance class. To use Steamworks you should create a new Blueprint based on Steam Game Instance or use the provided BP\_Steam\_Game\_Instance.

<figure><img src="../../.gitbook/assets/image (862).png" alt=""><figcaption></figcaption></figure>

## Configuration

You can adjust the behaviour of the Initialize Steam API function using the Class Defaults

<figure><img src="../../.gitbook/assets/image (863).png" alt=""><figcaption></figcaption></figure>

### Callback Frequency

Expressed in seconds this is the time between Run Callback calls. This is an important value as it dictates how frequently messages from Valve's Steam will be invoked as callback delegates in your game. This impacts all asynchronous features of Steam which is most of them.

The system will clamp this value to be between 0.1 and 0.01 e.g. 10Htz to 100Htz the typical range being more frequently 30Htz to 60Htz

### App ID

Only used for client API initialization this value is the App ID Valve issued you when you signed up for and paid for your Steam application fee. The value of 480 is the test App ID provided by Steam aka Spacewars but should be replaced with your own App ID as soon as you have it.

We use this value on initialisations to check if the app requires a restart and if so we will restart the app from the Steam client. You can learn more about this in our [steam\_appid.txt](../../steam/steam\_appid.txt.md) article.

### IP

Only used for game server API initialization this value is the string representation of the server's IP address. Generally only relevant when using Steam Game Server browser and connecting via IP/Port

### Game Port

Only used for game server API initialization this value is the port that will be used for connections.

### Query Port

Only used for game server API initialization this value is the port that will be used by Steam Game Server Matchmaking and similar queries

### Mode

Only used for game server API initialization this value indicates the authentication mode the server should run in ... typically Authentication or Authentication & Secure.

### Version

Only used for game server API initialization this value is used with Steam Game Server browser to indicate the version of the server and is expected to be in the form of #.#.#.#

## Initialization

<figure><img src="../../.gitbook/assets/image (864).png" alt=""><figcaption></figcaption></figure>

You will notice that initialization does require the use of a few nodes. The main node here is the Initialize Steam API function node. This will read the configuration you have provided from the Steam Game Instance and initialize Steam API for you. It will always initialize Steam Client API endpoints when executing on a client or listen server and will always initialise Steam Game Server API endpoints when executing on a dedicated server aka a "headless" server.

If you are building a dedicated server you will likely want to read the server configuration from some external source prior to calling this node.

The output of the node will indicate success or failure. If you are initializing for a client/listen server it may also indicate "Should Restart". This is a feature of Steam API, if the game was not launched from the Steam client then it will attempt to relaunch from the Steam client ... so if this is true you should close the game as Steam will be relaunching it from the Steam client its self.

Finally, we call a few event handlers so we can better organize our nodes.

## Events

<figure><img src="../../.gitbook/assets/image (865).png" alt=""><figcaption></figcaption></figure>

### Should Restart

This occurs in the event that the game was not launched from the Steam client. It indicates that Steam API is attempting to relaunch the game from the Steam client and thus this instnace of the game should be closed.

### Failed to Initialize

This generally only happens if your user isn't logged into Steam, doesn't have Steam installed at all or doesn't own the game and thus the API can't initialize. In this case, you should generally notify the user of this issue and its common causes and then close the game gracefully.

### Bootstraping

The Bootstrap Your Game Here is the ideal place to warm up your game systems and runs right after Steam API has successfully initialized. This is where you would enable Steam Input, find your leaderboards, load system settings, read the player's inventory and initialise any additional game systems relevant to your game.
