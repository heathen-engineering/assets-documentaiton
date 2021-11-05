---
description: Understanding Steam DLC and the Heathen Engineering tool kit
---

# Downloadable Content

{% hint style="warning" %}
#### Understanding Steam DLC

Its important to understand the proper usage of DLC. Most of this is a matter of configuration in the Steam Developer Portal. Please carfully and fully read the documentaiton for the feature. It can be found here [https://partner.steamgames.com/doc/store/application/dlc](https://partner.steamgames.com/doc/store/application/dlc)
{% endhint %}

![](<../../../.gitbook/assets/image (13).png>)

The Downloadable Content Object helps you track the status of DLC. Once you create the object from the Settings object, you will only need to enter the App ID. All other data will be quried at run time.

{% hint style="danger" %}
Remember users will use tools such as trainers to modify your games internal memory state. In the case of DLC they can alter the internal state such that "Is Subscribed" or other fields are "true" when they shouldn't be. To reduce the potential for this exploit its strongly recommended to use the method call approach as shown below.
{% endhint %}

## Examples

These examples assume you have a reference to your DLC object named leaderboard. To create such a reference you can do the following any mono behavior and simply drag a reference to it in the Unity inspector.

### Referencing a DLC

```csharp
public DownloadableContentObject dlc;
```

### Check if owned and subscribed

Check if the user is "subscribed" to this DLC. this indicates the user owns the DLC and has it enabled.

```csharp
if(dlc.GetIsSubscribed())
{
  Debug.Log("The user owns and has enabled this DLC");
}
```

### Open the store to this DLC

Open the overlay to the store page of this DLC

```csharp
dlc.OpenStore();
```

{% hint style="warning" %}
Note the OpenStore command opens the Steam Overlay, which does not work well in Unity Editor.
{% endhint %}

### Is DLC installed

While most games already include all there content and use DLC as a license check to unlock existing features, Steam does support the older approach of DLC being an additional install.

&#x20;To check if the DLC is installed

```csharp
if(dlc.GetIsInstalled())
{
  Debug.Log("This DLC is installed");
}
```

### Get installation directory

To get the install directory

```csharp
var path = dlc.GetInstallDirectory();
```

### Start DLC Install

To start the install process

```csharp
dlc.InstallDLC();
```

### Uninstall DLC

To uninstall the DLC

```csharp
dlc.UninstallDLC();
```

### Get install progress

To check install progress

```csharp
var percentCompelte = dlc.GetDownloadProgress();
```

### When was DLC purchased

Check the date time the DLC was purchased

```csharp
DateTime dateTime = dlc.GetEarliestPurchaseTime();
```
