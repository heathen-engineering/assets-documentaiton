---
description: Access the Steam Clan aka Steam Group system with Heathen's Steam API
---

# Clans

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
public static class API.Clans
```

The whole of the clans system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Clans.Client
```

### What is clan?

Also known as a Community Group, Steam lets user's create there own social groups, these could be groups of active players similar to a guild in an MMO or simply an interest group e.g. a collection of Steam users with similar interests. You can search the existing community groups here:

{% embed url="https://steamcommunity.com/search/groups" %}
Search For Community Groups
{% endembed %}

### What can it do?

You can list the clan owner, its officers, open the clan chat in overlay or join the clan's chat in game. The most common use game developers look for and the most complex is to join the clan chat in game.

### Related Componenets

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/clan-chat-director" %}

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/clan" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/clan-chat-msg" %}

## How To

### Create a Clan / Group

This cannot be done from within the Steam API at current you can however direct your player's to the approprete location in Steam to create there own clans.

> [https://steamcommunity.com/actions/GroupCreate](https://steamcommunity.com/actions/GroupCreate)

The above URL can be passed into the Steam Overlay

```csharp
API.Overlay.Client.ActivateGameOverlayToWebPage
    ("https://steamcommunity.com/actions/GroupCreate");
```

### Get Clans / Groups

Return an array of the clans the user is a member of

```csharp
Clan[] clans = API.Clans.Client.GetClans();
```

The Clan object contains various helpful members such as Clan.Name, ClanOwner, Clan.JoinChat and more.

### List Clan officers

Using the Clan object

```csharp
UserData[] officers = clan.Officers
```

