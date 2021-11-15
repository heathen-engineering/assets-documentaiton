# Leaderboard Object

## Definition

```csharp
public class LeaderboardObject : ScriptableObject
```

Represents a Steam Leaderboard and is used by the [Steam Settings](steam-settings.md) object to initalize the Leaderboard system.

You create leaderboard objects through thee Steam Settings object by clicking the <mark style="color:green;">+ New</mark> button in the leaderboards list.

![](<../../../.gitbook/assets/image (184).png>)

From the Steam Settings you can mark the leaderboard as create if missing by ticking the toggle to the left of the name.

![](<../../../.gitbook/assets/image (152).png>)

![](<../../../.gitbook/assets/image (165).png>)

You can specify the number of detail entries the board should handle by entering a number in the Details field

{% hint style="warning" %}
Each board can handle up to 64 details and no more than that
{% endhint %}

If your marking your board as Create if Missing e.g. you have ticked the box as indiacted above then you should also set the display type and sorting order by selecting the leaderboard in your Steam Settings and editing its values.

![](<../../../.gitbook/assets/image (153).png>)

{% hint style="danger" %}
None is an available but invalid option for both settings



Why even show it if its invalid, ask Valve, its part of the enums they provide so we expose it.
{% endhint %}

## Fields and Attributes

| Type                    | Name             | Comment                                                              |
| ----------------------- | ---------------- | -------------------------------------------------------------------- |
| bool                    | createIfMissing  | Should the board be created if missing                               |
| ELeaderboardSortMethod  | sortMethod       | If creating a board what sort methhod should be applied              |
| ELeaderboardDisplayType | displayType      | If creating a board what display type should it have                 |
| string                  | leaderboardName  | The name of the board as defined in the Steam Developer Portal       |
| int                     | maxDetailEntries | How many detail entries should be allowed on entries from this board |
| SteamLeaderboard\_t     | leaderboardId    |                                                                      |
| bool                    | Valid            | is the board found and ready for use                                 |
| int                     | EntryCount       | number of records on this board                                      |

## Methods

### Get User Entries

```csharp
public void GetUserEntry(callback);
```

Returns the entry for the local user

```csharp
public void GetEntries(request, start, end, callback);
```

Get a range of entries matching the reequest type and range of data

### Register

```csharp
public void Register();
```

Finds or creates the board according to configuration values. This is handled by the internal system for all boards defined at development time but must be called manually if you define this object at run time.

### Upload Score

```csharp
public void UploadScore(score, method, callback);
```

```csharp
public void UploadScore(score, details, method, callback);
```

Uploads a given score and optionally includes details

### Attach File

```csharp
public void AttachUGC(fileName, jsonObject, encoding, callback);
```

This will save the provided object to Steam Remote Storage by using JsonUtility to serialize it according to the encoding method.&#x20;

Once saved to Remote Storage it will be shared  yielding a UGC Share File which will be attached to this user's current leaderboard entry.
