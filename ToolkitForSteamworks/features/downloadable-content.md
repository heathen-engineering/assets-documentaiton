# Downloadable Content

## Introduction

Steam Downloadable Content aka DLC allows you to sell expansions, seasons and other add-ons for your game through the Steam store and reliably and securely detect when a user owns that add-on

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/store/application/dlc](https://partner.steamgames.com/doc/store/application/dlc)

</details>

## Quick Start

First, you need to create your DLC on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

### Create

Log into your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../.gitbook/assets/image (216).png" alt=""><figcaption></figcaption></figure>

From there scroll down until you find the All DLC section and click Add New DLC button

<figure><img src="../.gitbook/assets/image (217).png" alt=""><figcaption></figcaption></figure>

Populate the form with the names of the DLC you would like to create making sure to start the name with the name of your game. For example, our game's name is Túatha Legends so we might a DLC something like Túatha Legends - The Iron King

### Publish

You \*\***MUST**\*\* publish your changes in the Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

## Examples

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

coming soon

## C\#

```csharp
if(SteamTools.Game.DLC.ticket_test_DLC.IsSubscribed)
{
    // The DLC is owned and enabled
}

// Get the DLC's name as the user sees it
string displayName = SteamTools.Game.DLC.ticket_test_DLC.Name;

// Open the Steam Overlay to this DLC's store page
SteamTools.Game.DLC.ticket_test_DLC.OpenStore();
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
Modern DLC are not content that you download, they are far more often locked content that you unlock through a purchase.

### Is Subscribed

<figure><img src="../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

In Steam, you don't "own" a game or app; you are "subscribed" to it. So, to check for ownership of a given DLC, use the Steam Is Subscribed App node.

#### For C++ source:

Assuming the app is a valid `AppId_t` note that `AppId_t` is a Steamworks `typedef` for `uint32`.

```cpp
bool result = SteamApps()->BIsSubscribedApp(app);
```

### Iterate over DLC

<figure><img src="../.gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>

It's often handy to iterate over all your DLC, such as to list them in the game or open the Overlay to the store pages. We have provided several nodes to help you do just that.

#### For C++ source:

You can get the count of all the DLC for the app via&#x20;

```cpp
int32 count = SteamApps()->GetDLCCount();
```

With that, you can iterate through each and fetch details about a DLC via

```cpp
AppId_t appId;
bool available;
char name[128];
if (SteamApps()->BGetDLCDataByIndex(index, &appId, &available, name, 128))
{
    //Use the results
}
```

### DLC Installation

<figure><img src="../.gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>

Finally, if you are doing traditional DLC that is installed we provide you with node to check for installation, start the installation and uninstall. Note that install and uninstall is a request, Steam will attempt it if it can but if the user doesn't own the DLC, or the files are locked by the game running them, etc. then it may not complete.

#### For C++ source:

To install DLC

```cpp
SteamApps()->InstallDLC(appId);
```

Check if a DLC is installed

```cpp
bool result = SteamApps()->BIsDlcInstalled(appId);
```

Uninstall a DLC

```cpp
SteamApps()->UninstallDLC(appId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Comming Soon
{% endtab %}
{% endtabs %}

