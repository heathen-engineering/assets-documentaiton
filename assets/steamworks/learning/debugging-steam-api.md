# Debugging Steam API

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

Heathen provides a powerful inspector that will show you the states and values of all Steam API artifacts configured for your project. To Access the inspector simply open the Steamworks > Inspector menu.

![Opening the inspector](<../../../.gitbook/assets/image (20).png>)

{% hint style="warning" %}
#### IMPORTANT

The inspector's data only populate while the simulation is running.
{% endhint %}

## Step 1

The Home page of the inspector displays core values for your user and the app its self. This is the first place you should check, and you should do the following

1. Is the Initalization Satus = Initalized?
2. Is the Listed App ID what I expect it to be?
3. Is the Reported App ID the same as the Listed App ID
4. Is the steam\_appid.txt the same as the Listed App ID
5. Is the displayed user me / who I expect it to be

![](<../../../.gitbook/assets/image (151).png>)

If you answered no to any of the above questions your issue is on step 1. That is your not configured correctly to initialize Steam and or you do not have the Steam client up and running with a valid user logged in.

If for example you find that the App ID does not match then what you most likely did was to change the App ID in the Steam Settings file but did not fully shut down Unity, Visual Studio and absolutely everything else that might have mounted it; e.g. Unity, Visual Studio or any related process.

The reason this happens is that Valve will not release app initialization until every process that mounted its handles has closed. This is the single most common issue we have reported.

## Stats

![](<../../../.gitbook/assets/image (173) (1).png>)

You can use the Stats tab to view and update the value of all registered stats

## Achievements

![](<../../../.gitbook/assets/image (179) (1).png>)

You can use the Achievements tab to view and unlock/reset all registered achievements

## Leaderboards

![](<../../../.gitbook/assets/image (170) (1) (1).png>)

You can use the Leaderboard's tab to view your score and rank on all registered leaderboards. Leaderboards while one of the simplest aspects of Steam API are also one of the more fragile aspects.

Common issues seen with Leaderboards include

1. You have the sort order set incorrectly
2. You have the leaderboard set to trusted only
3. You made changes in Steam Developer Portal and didn't publish them

We do on occasion see leaderboards "break", this is typically a problem when you change values on the board or delete a board and make a new one with the same name but different settings. In most cases its easiest and best to simply make a new board with a new unique API name.&#x20;

If you need to repair a board that is misbehaving you will need to contact Valve's support as these are backend features Heathen can not see nor effect.

## Downloadable Content

![](<../../../.gitbook/assets/image (181) (1).png>)

You can view the subscription status of all DLC in the DLC tab

## Inventory

![](<../../../.gitbook/assets/image (164) (1) (1).png>)

The inventory tab will display all the items registered to your game and provides tools for clearing and granting each item

## Lobbies

![](<../../../.gitbook/assets/image (185).png>)

The lobbies tab will populate a sub page for each detected lobby and will display the list of members and the lobby's metadata.
