---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# ScriptableObject Initialization

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Initialize Steam API with this [Steam Settings](../classes-and-structs/steam-settings/) object. You do not require the use of any component scripts and thus do not require the use of any GameObjects to use this method. You will need to define your [Steam Settings](../classes-and-structs/steam-settings/) object and then use it to initialize the API by calling its `Initialize()` method.

```csharp
using HeathenEngineering.SteamworksIntegration;

namespace YourNameSpace
{
    public class SomeScriptOfYours : MonoBehaviour
    {
        [SerializeField]
        private SteamSettings settings;
    
        void Start()
        {
            //This is all that is required
            settings.Initialize();
        }
    }
}
```

In the above example we do use a MonoBehaviour but that is not required. All that is required is that you call the Initialize method on the Steam Settings object you wish to initialize.

## Steam Settings

[Learn more about the Steam Settings object here](../classes-and-structs/steam-settings/).

Create a new Steam Settings object in your project folder by right clicking in your project tab and selecting\
**Create > Steamworks > Settings**

![](<../../../.gitbook/assets/image (158) (1) (1) (1) (1).png>)

The only value you "must" set is the Application Id

### Application Id

Enter your app ID in the Application Id field**.**  If you don't have an application ID just yet that's fine you can work with the test App ID 480 however there will be some limitations.&#x20;

{% hint style="info" %}
You obviously cannot deploy your app without an App ID

You cannot create your own achievements, stats or other artefacts without your own ID



Valve issues you an App ID when you pay your application fee. If you don't have your own ID yet you can use App ID 480 as a test ID. Heathen's samples and demos all use App ID 480.
{% endhint %}

### Artifacts

<figure><img src="../../../.gitbook/assets/image (3) (5).png" alt=""><figcaption></figcaption></figure>

The Steam Settings object can be used to reference all of your Steam "artifacts" such as Input Fields, [Stats](../../../company/steam/steamworks/stats-object.md), [Leaderboards](../../../company/steam/steamworks/leaderboard-object/), [Achievements](../../../steam/achievements.md), [DLC ](../../../steam/downloadable-content-object.md)and [Inventory items](../../../company/steam/steamworks/inventory/). For many of these artifact types you can define them in the Steam Developer Portal as you normally would and then use the "Import" button to pull them into your project.

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

The Steam Game Server Configuration lets you configure the details of your game server as it will be seen by Steam. This is only relevant for server builds that will be initializing and logging on as a "[Steam Game Server](../../../company/steam/steamworks/multiplayer/game-server-browser/)"

If you set the "Auto Logon" feature to false you will need to call LogOn for the server when your ready for it to log on which is done via the [API.App.Server.LogOn()](../api/app.server.md#logon) method.

This is most commonly done when you want to prevent the server from registering itself on the Steam Game Server browser until after you have made it ready such as after you have "StartServer" called on your HLAPI of choice and have configured the server making it ready for connections.

[You can learn more about the configuration fields here](../classes-and-structs/steam-game-server-configuration.md).
