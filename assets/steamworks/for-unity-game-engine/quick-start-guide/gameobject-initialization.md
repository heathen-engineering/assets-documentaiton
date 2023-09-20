# GameObject Initialization

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Initialize Steam API with a simple component script attached to a GameObject of your choice. You can use the [Steamworks Behaviour](../../unity/components/steamworks-behaviour.md) or the [Steamworks Creator](../../unity/components/steamworks-creator.md) to handle initialization for you. In both cases however you do need to first create and configure a [Steam Settings](../../unity/scriptable-objects/steam-settings/) object. Once you have your Steam Settings object defined and configured you can apply it to the [Steamworks Behaviour](../../unity/components/steamworks-behaviour.md) or [Steamworks Creator](../../unity/components/steamworks-creator.md) depending on which you choose to use.

## Steamworks Behaviour

[Learn more about the Steamworks Behaviour here](gameobject-initialization.md#steamworks-behaviour).

Steamworks Behaviour is used to initialize a Steam Settings object on startup of the game and provides access to a few system level events such as Initialized.&#x20;

You should only ever have 1 Steamworks Behaviour in your game.

You should NOT define your Steamworks Behaviour in your "main menu" or "title" scene as these scenes get loaded and reloaded multiple times. Instead you should use a "[bootstrap](../../../../company/design/bootstrap-scene.md)" scene and place the behaviour and all other system level objects there. If you cannot or do not want to use a bootstrap setup then see the Steamworks Creator.

## Steamworks Creator

[Learn more about the Steamworks Creator here](../../unity/components/steamworks-creator.md).

This is a simple script behaviour that checks if the Steam API is already initialized or not. If it is not it will create a new Steamworks Behaviour and optionally mark it as Do Not Destroy On Load.&#x20;

This behaviour is here to help developers that are using the old approach to scene architecture and are not using a [bootstrap process](../../../../company/design/bootstrap-scene.md). You can safely put the Steamworks Creator in every scene of your game as it will only work if its required to do so.

{% hint style="warning" %}
This is not an efficient or robust way of architecting a game. We only support it as it is very common with new Unity developers.\
\
We very strongly encourage you to create a [bootstrap process](../../../../company/design/bootstrap-scene.md) for your game in which case the proper place for Steam initialization is as part of that [bootstrap process](../../../../company/design/bootstrap-scene.md).
{% endhint %}

## Steam Settings

[Learn more about the Steam Settings object here](../../unity/scriptable-objects/steam-settings/).

Create a new Steam Settings object in your project folder by right clicking in your project tab and selecting\
**Create > Steamworks > Settings**

![](<../../../../.gitbook/assets/image (158) (1) (1) (1) (1).png>)

The only value you "must" set is the Application Id

### Application Id

Enter your app ID in the Application Id field**.**  If you don't have an application ID just yet that's fine you can work with the test App ID 480 however there will be some limitations.&#x20;

{% hint style="info" %}
You obviously cannot deploy your app without an App ID

You cannot create your own achievements, stats or other artefacts without your own ID



Valve issues you an App ID when you pay your application fee. If you don't have your own ID yet you can use App ID 480 as a test ID. Heathen's samples and demos all use App ID 480.
{% endhint %}

### Artifacts

<figure><img src="../../../../.gitbook/assets/image (3) (5).png" alt=""><figcaption></figcaption></figure>

The Steam Settings object can be used to reference all of your Steam "artifacts" such as Input Fields, [Stats](../../../../company/steam/steamworks/stats-object.md), [Leaderboards](../../../../company/steam/steamworks/leaderboard-object/), [Achievements](../../../../company/steam/achievements.md), [DLC ](../../../../company/steam/steamworks/downloadable-content-object.md)and [Inventory items](../../../../company/steam/steamworks/inventory/). For many of these artifact types you can define them in the Steam Developer Portal as you normally would and then use the "Import" button to pull them into your project.

{% hint style="info" %}
The Unity Editor must be in "Play" mode for the import buttons to work.\
\
You can import

* Achievements
* Downloadable Content&#x20;
* <mark style="color:red;">\*</mark> Inventory Items <mark style="color:red;">\*</mark>



&#x20;_<mark style="color:red;">\*</mark> Note_\
Valve limits what information on Inventory Items can be imported. For example bundle content will not be imported. This is a deliberate limitation from Valve and cannot be worked around. In general you only need the item ID of an item so this should not be a problem in most use cases.
{% endhint %}

### Steam Game Server Configuration

The Steam Game Server Configuration lets you configure the details of your game server as it will be seen by Steam. This is only relevant for server builds that will be initializing and logging on as a "[Steam Game Server](../../../../company/steam/steamworks/multiplayer/game-server-browser/)"

If you set the "Auto Logon" feature to false you will need to call LogOn for the server when your ready for it to log on which is done via the [API.App.Server.LogOn()](../../unity-engine/api/app.server.md#logon) method.

This is most commonly done when you want to prevent the server from registering itself on the Steam Game Server browser until after you have made it ready such as after you have "StartServer" called on your HLAPI of choice and have configured the server making it ready for connections.

[You can learn more about the configuration fields here](../../unity-engine/objects/steam-game-server-configuration.md).
