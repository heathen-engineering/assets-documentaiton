---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# Unreal DLC

## Blueprints

Modern DLC are not actually content that you download, they are far more offten locked content that you unlock through a purchase.

### Is Subscribed

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

In Steam you don't "own" a game or app, you are "subscribed" to it. So to check for ownership of a given DLC, use the Steam Is Subscribed App node.

### Iterate over DLC

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

It's often handy to iterate over all your DLC such as to list them in the game or open the Overlay to the store pages. We have provided a number of nodes to help you do just that.

### DLC Installation

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Finally, if you are doing traditional DLC that is installed we provide you with node to check for installation, start the installation and uninstall. Note that install and uninstall is a request, Steam will attempt it if it can but if the user doesn't own the DLC, or the files are locked by the game running them, etc. then it may not complete.

## C++

### Is Subscribed

Assuming app is a valid `AppId_t` note that `AppId_t` is a Steamworks `typedef` for `uint32`.

```cpp
bool result = SteamApps()->BIsSubscribedApp(app);
```

### Iterate over DLC

You can get the count of all the DLC for the app via&#x20;

```cpp
int32 count = SteamApps()->GetDLCCount();
```

with that, you can iterate through each and fetch details about a DLC via

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
