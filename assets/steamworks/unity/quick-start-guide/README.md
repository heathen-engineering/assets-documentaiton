---
description: A quick start guide for those already comfortable with the basics.
---

# Quick Start

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Initalization

You have choices with how you handle initalization, the simples and most commonly used method is to define a Steam Settings object and use the Steamworks Behaviour to initalization and amange your Steam API integration as shown below

### Steam Settings

Create a new Steam Settings object in your project folder by right clicking in your project tab and selecting\
**Create > Steamworks > Settings**

![](<../../../../.gitbook/assets/image (158) (1) (1) (1) (1).png>)

### App Id

Enter your app ID in the Application Id field**.**  If you don't have an application ID just yet that's fine you can work with the test App ID 480 however there will be some limitations.&#x20;

{% hint style="info" %}
You obviously cannot deploy your app without an App ID

You cannot create your own achievements, stats or other artefacts without your own ID



Valve issues you an App ID when you pay your application fee. If you don't have your own ID yet you can use App ID 480 as a test ID. Heathen's samples and demos all use App ID 480.
{% endhint %}

### Steamworks Behaviour

Create a [Steamworks Behaviour](broken-reference) object in your [bootstrap scene](../../../../company/concepts/design/bootstrap-scene.md) or similarly appropriate location; and drag your Steam Settings object into the provided field.

![](<../../../../.gitbook/assets/image (161) (1) (1) (1) (1) (1) (1).png>)

Congratulations, you are now integrated with the Steam APIs. If you run the simulation, you will see that the Steam API initializes and is ready for use.

{% hint style="warning" %}
It is of course up to you to perform any required validation checks ... that is you MUST make sure Steam is finished initializing before you try to use it and that it did in fact initialize without error. \
\
The [Steamworks Behaviour](../components/steamworks-behaviour.md) has events exposed to report initialization or error or you can test via Boolean using [SteamSettings.Initialized](../scriptable-objects/steam-settings/#initialized)
{% endhint %}

## Advanced

### Steam Settings

Steam Settings can be used to initialize the Steam API without using a component script at all. This is useful for people using Unity's Entity Componenet system who do not want to use a component script.

You will still need a Steam Settings object as this defines your various "artifacts" such as stats, achievements, input fields, inventory items and more. Once defined you can simply call&#x20;

```csharp
public SteamSettings mySettings;
mySettings.Intitalize();
```

This will initialize the Steam API and run its update loop via a background worker. No MonoBehaviour will be involved at all.

### API.App

For users that are allergic to Unity's ScriptableObjects you can use Heathen's API's to initialize and manage the API. The advantage of using Steam Settings is management of your various Steam related artifacts such as Leaderboards, Achievements, etc. however if you wish to go all code and no Unity objects at all ... we have you covered.

```csharp
//For a client initialization
API.App.Client.Initialze(AppData appId);

//For a server initialization
API.App.Server.Initialize(AppData appId, SteamGameServerConfiguraiton config);
```

You can learn more about [AppData ](../../data-layer/app-data.md)and [SteamGameServerConfiguraiton ](../components/steam-game-server-events.md)in our knowledge base.

## Networking

{% embed url="https://kb.heathenengineering.com/assets/steamworks/guides/multiplayer" %}

{% hint style="success" %}
Steamworks Complete and whatever HLAPI you chose to work with have no impact on each other at all. You will use Steamworks and your HLAPI of choice exactly the same with as you would without the other.
{% endhint %}

### Do I need Steamworks Complete?

You do not "require" Steamworks Complete in order to use Mirror, FishNetworking or NetCode for GameObject's or any other Steam transports. Those transports like our self work with Steamworks.NET directly.

That said you will need to initialize, configure and manage the Steam API before SteamNetworking interfaces can be used. Our Steamworks Complete and Steamworks Foundation packages make working with Steam API simple and stable. If you do not use Steamworks Complete or Foundation you would need to use the raw Steam API to initialize and configure your Steam API integration your self before your HLAPI could use the Steam transports.

### Examples?

Where can I find examples on using Steamworks Complete and (the HLAPI I chose)?

You cant because their is no need. Both Steamworks Complete and your HLAPI of choice work exactly the same rather or not the other exists. Thus we do not have an example of using (your HLAPI of choice) along side our Steamworks Complete.&#x20;

If you want to see an example of using your HLAPI of choice with your HLAPI's Steam transport then you should contact them. We have links to [Fish Networking, Mirror and NetCode for GameObjects in our articles](../installation/networking-integrations.md) but any HLAPI that works with Steamworks.NET properly will work.

If your looking for examples on how to initialize, configure and use Steam API (in general) you will find various samples in the provided [samples scenes](../../../physkit/learning/sample-scenes/) and examples throughout our knowledge base.

If your trying to wrap your head around creating a [multiplayer game on the Steam platform](broken-reference), we have an article for that as well. That article is not specific to any given HLAPI because the HLAPI you choose has no impact on the concepts involved.
