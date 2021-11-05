---
description: This section outlines the upcoming improvements to Steamworks
---

# Coming Soon

"Work In Progress" (WIP) documents for upcoming updates to Heathen's Steamworks integration are indicated with a NOTE such as.

{% hint style="warning" %}
Coming Soon

This will be released with Patch 13 and is expected late 2021 to early 2022 as a free update to Steamworks V2
{% endhint %}

This can be used for users current'y using a preview build of Steamworks or just to get a sneak peek at upcoming features.

## 2019.2.13.X

### Summary

This patch will introduce a new more efficent wrap around the raw Steam API. The main driver for this signifigant change is

1. Improve performance and memory use
   1.  Reduce the use of managed reference types

       This reduces GC impact and should make it easier to use in systems like DOTs ... it also means Unity's burst compiler can better optimize though this is a minor impact.
   2.  Direct use of Steam's local cashe

       Prior versions cashed data in Unity's memory this version reads more directly from Steam's cash reducing Unity's memory and insuring there are no sync issues as there is no sync
   3.  Less duplication

       Prior versions duplicated some callbacks and events in the name of ease of discovery. This has been adjusted such that any given callback or event has exsactly 1 instance. The same applies to processes
   4.  Reduce or remove need for loops

       Prior versions simplified Steam's callback/callresult using UnityEvents mainly which required some loop checks that did take some measure of clock time. The new model uses Actions directly on calls that support async operation meaning true async use, no need for IEnumerable, no Coroutines e.g. no loops.
   5.  Image Management

       In prior versions unintended use of some features could cause images such as Achievement icons, user avatars, etc. to become duplicated in memory with no simple way to clean them up. The new model will assuredly not duplicate them in Unity memory and provides easy to use tools to free them.
2. Discoverability & Ease of Use
   1.  Wrapped every Steam feature in the API namespace e.g. API.Friends API.Leaderboard, etc.

       This lets you use in IDE tools like intelisence to discover Stem features
   2.  Every funciton and callback represents

       Every API, Function and Callback/CallResult is represented in its C# form with full Steam documentation added to the comments and remarks
   3. New Sample Scenes and scripts covering every interface and funciton
   4. Improved documentaiton as seen here :)
   5.  Implicite conversions for common ID types

       UserData, Lobby, LobbyMember, DLC, etc.
3. Utility and Debugging
   1. Expanded Steamworks Inspector
      1. View, unlock and relock achievements in editor
      2. View, set and rest stats in editor
      3. View, and upload scores to leaderboards in editor
      4. View, grant and clear inventory items in editor
      5. View DLC ownership status in editor
      6. View connect lobbies and there metadata in editor
   2. New Settings Inspector
      1.  Import common artifacts directly form Steam Portal&#x20;

          (Achievements, DLC and Inventory Items)
      2. All artifacts managed as children of the settings object
      3.  All artifacts edited directly in the Steam Settings

          No need to edit in a seperate window now
4.  Remove Dependency on UI frameworks&#x20;

    This means we no longer ship any compound UnityEngine.UI componenets. We do still provide you with easy to use tools such as SetUserAvatar but these are highly modular so you can use TMPro Text, uGUI Text, IMGUI Text, UIElements Text or anything else you like along side.

### Changes

#### New APIs

* App
* Authentication
* Clans
* Friends
* Input
* Inventory
* Leaderboards
* Matchmaking
* Overlay
* Parties
* RemotePlay
* RemoteStorage
* Screenshots
* StatsAndAchievements
* User
* Utilities
* Voice

#### Additions

1. AchievementAttributes
2. AvgRateStatObject
3. Clan
4. ClanChatMessage
5. ClanChatUserLeaveData
6. DownloadableContent
7. ExtendedItemDetail
8. FavoriteGameData
9. FriendDialog
10. InventoryExchangeRecipe
11. InventoryItemDefinition
12. InventoryItemProperty
13. InventoryItemType
14. InventoryManager
15. InventoryResult
16. ItemTag
17. LanguageCodes
18. LeaderboardRankChangeData
19. LeaderboardScoresDownloaded
20. LobbyChatDirector
21. LobbyChatMsgData
22. LobbyGameServerData
23. LobbyManager
24. OverlayDialog
25. OverlayManager
26. PartyBeaconDetails
27. RemoteStorageFile
28. RemoteStorageManager
29. SampleRateMethod
30. SetUserAvatar
31. TMProSetUserName
32. UGUISetUserName
33. ValvePriceCategories
34. VoiceRecorder
35. VoiceStream

#### Changes

1. AchievementObject
2. Authentication
3. DataModel
4. DownloadableContentObject
5. ExtendedLeaderboardEntry
6. FloatStatObject
7. IntStatObject
8. LeaderboardObject
9. Lobby
10. StatObject
11. SteamSettings
12. SteamworksBehaviour
13. SteamworksCreator
14. UserData

#### Depricated

A signnifigant number of objects have been depricated as there funcitonality has been replaced by the new API tools and new simplified managers.

1. `Authentication`, moved to `API.Authentication`
2. `AvatarRawImage`, replace dy `SetUserAvatar`
3. `SteamUserFullIcon`, see the new samples
4. `SteamUserIconButton`, see the new samples
5. `BasicLeaderboardEntry`, no longer used
6. `ClanTools`, moved to `API.Clans`
7. `CraftingRecipe`, replaced by funcitonality in the new `InventoryItemDefinition`
8. `ExchangeItemCount`, replaced by funcitonality in the new `InventoryItemDefinition`
9. `FileDataModel`, no longer used, see `API.RemoteStorage` and `DataModel`
10. `GenerateItemCount`, replaced by funcitonality in the new `InventoryItemDefinition`
11. `IconicLobbyChatMessage`, no longer used, see `SetUserAvatar` componenet
12. `InventoryItemBundleDefinition`, replaced by funcitonality in the new `InventoryItemDefinition`
13. `InventoryItemDefinitionCount`, replaced by funcitonality in the new `InventoryItemDefinition`
14. `InventoryItemPointer`, replaced by funcitonality in the new `InventoryItemDefinition`
15. `InventoryItemPointerCount`, replaced by funcitonality in the new `InventoryItemDefinition`
16. `ISteamworksLobbyManager`, moved to `API.Matchmaking`
17. `ItemExchangeRecipe`, replaced by funcitonality in the new `InventoryItemDefinition`
18. `ItemGeneratorDefinition`, replaced by funcitonality in the new `InventoryItemDefinition`
19. `LeaderboardDisplayList`, no longer used see the new samples
20. `LeaderboardEntryDisplay`, no longer used see the new samples
21. `LobbyChat`, replaced by `LobbyChatDirector`
22. `LobbyChatMessage`, no longer used see the new samples
23. `LobbyChatMessageData`, no longer used see the new samples
24. `LobbyChatMessageEvent`, replaced by `LobbyChatMsgEvent`
25. `LobbyDisplayList`, no longer used see the new samples
26. `MatchmakingTools`, replaced by `API.Matchmaking`
27. `RemoteStorageDataFile`, no longer used, see `API.RemoteStorage`
28. `RemoteStorageSystem`, no longer used, see `API.RemoteStorage`
29. `SteamClan`, replaced by `Clan`
30. `SteamDataFileList`, no longer used, see the new samples
31. `SteamDataFileRecord`, no longer used
32. `SteamDataFileRecordEditor`, no longer used
33. `SteamworksInventoryTools`, replaced by `API.Inventory`
34. `SteamworksRemoteStorageEditor` , no longer used
35. `TagGeneratorDefinition`, replaced by funcitonality in the new `InventoryItemDefinition`
36. `TagGeneratorValue`, replaced by funcitonality in the new `InventoryItemDefinition`
37. `UnityFileShareResultEvent`, no longer used, see `API.RemoteStroage`
38. `UnityLeaderboardEntryUpdateEvent`, no longer used see `API.Leaderboards`
39. `VoiceManager`, replaced by `VoiceRecorder` and `VoiceStream`&#x20;

``
