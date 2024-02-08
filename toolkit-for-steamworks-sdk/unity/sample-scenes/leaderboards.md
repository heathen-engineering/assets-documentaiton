---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Leaderboards

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

<figure><img src="../../../.gitbook/assets/image (1) (5).png" alt=""><figcaption></figcaption></figure>

The Leaderboard sample scene demonstrates the read, write and display of Leaderboard data. The sample scene doesn't use any custom code and works "code free" using standard Heathen tools.

## Configuration

### Steamworks Behaviour

Located on the Manager GameObject in the scene root. [Steamworks Behaviour](../components/steamworks-behaviour.md) is required for the Steam API to work at all. Typically this would be in your [Bootstrap scene](../../../company/design/bootstrap-scene.md) however for the case of these samples which are meant to be ran in editor we place them here.

In the case of this sample we are using the [Evt Steam Initialized](../components/steamworks-behaviour.md#evt-steam-initialized) event on the behaviour to trigger the initial query on the Leaderboard Manager and refresh the Leaderboard User Entry.

### Leaderboard Manager

Located on the Canvas > Leaderboard Scroll View GameObject. The[ Leaderboard Manager](../components/leaderboard-manager.md) is responsible for managing a specific leaderboard and facilitates queries against that board.

The 3 buttons arranged above the display area simply call methods on the [Leaderboard Manager](../components/leaderboard-manager.md) to start query processes. The [Leaderboard Manager's Evt Query Completed](../components/leaderboard-manager.md#evtquerycompleted) event will be raised as each query completes and will call the [Leaderboard UI List's Display](../ui-components/leaderboard-ui-list.md#display) method causing the results to be displayed in the UI.

### Leaderboard UI List

Located on the Canvas > Leaderboard Scroll View GameObject. The [Leaderboard UI List](../ui-components/leaderboard-ui-list.md) is responsible for consuming query results and displaying the records on the UI.&#x20;

This is done by instantiating the Leaderboard Entry UI Record which uses the [LeaderboardEntryUIRecord](../ui-components/leaderboard-entry-ui-record.md) component to set UI elements according to the provided [LeaderboardEntry](../classes-and-structs/leaderboard-entry.md) value.&#x20;

### Leaderboard Entry UI Record

Located on the Canvas > Leaderboard Scroll View > Template > Leaderboard Entry UI Record GameObject. The [Leaderboard Entry UI Record](../ui-components/leaderboard-entry-ui-record.md) is instantiated by the Leaderboard UI List for each record it is provided.

## Developer Cheat Box

At the bottom of the screen you will see a red box with a few few self explanatory buttons. Those buttons use the [LeaderboardObject ](../scriptable-objects/leaderboard-object.md)to clear or update the score of the user on the leaderboard in question.

To the right you will notice a display that updates in real time as the user's score is changed. The Developer Cheat Box > User Leaderboard Entry GameObject is using the [LeaderboardUserEntry](../components/leaderboard-user-entry.md) component to update the score and rank label's for the user on this board. This component reacts to changes on the board and updates the values as required and can be refreshed on demand if desired.

## Testing

Assuming you are using an unmodified version of the sample scene and Steam Settings you will see messages appear in the Unity Editor Console log detailing each step of the initialization process.

<figure><img src="../../../.gitbook/assets/image (15) (1) (3).png" alt=""><figcaption><p>Example initialization messages</p></figcaption></figure>

In the event of an error details will be listed here along with troubleshooting guidance. In the event you require support please select the first error message in the log and press \[Ctrl + C] this will copy the full message and its stack trace to your clipboard. You can then paste that error into [Discord chat](https://discord.gg/eVVgM36) for live support or into a support email or similar.

Aside from the console output you can use the "Developer Cheat Box" to clear your score and upload score at 5 or 10 increments. The green buttons located at the top of the board allow you to query the boards top 10, to query only your friends or to query the entries near your own and are demonstrations of the various queries available all ran code free.
