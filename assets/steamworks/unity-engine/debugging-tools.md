# Debugging Tools

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Enable Debugging

![Toggle this on](<../../../.gitbook/assets/image (3) (1) (3).png>)

When toggled on Heathen's tools will write additional verbose information in particular around initialization which is the most common point of error. If you have not finished testing and are not building a fully tested, production ready, release build ... then you should have this turned on.

## Steamworks Inspector

Heathen provides a powerful inspector that will show you the states and values of all Steam API artefacts configured for your project.&#x20;

To Access the inspector simply open the **Window > Steamworks Inspector** menu.

or

![Click the button in Steam Settings](<../../../.gitbook/assets/image (5) (3).png>)

{% hint style="warning" %}
#### IMPORTANT

The inspector's data only populate while the simulation is running.
{% endhint %}

The Home page of the inspector displays core values for your user and the app its self. This is the first place you should check, and you should do the following

1. Is the Initialization Status = Initialized?
2. Is the Listed App ID what I expect it to be?
3. Is the Reported App ID the same as the Listed App ID
4. Is the steam\_appid.txt the same as the Listed App ID
5. Is the displayed user me / who I expect it to be

![](<../../../.gitbook/assets/image (151) (1).png>)

If you answered no to any of the above questions your issue is on step 1. That is your not configured correctly to initialize Steam and or you do not have the Steam client up and running with a valid user logged in.

If for example you find that the App ID does not match then what you most likely did was to change the App ID in the Steam Settings file but did not fully shut down Unity, Visual Studio and absolutely everything else that might have mounted it; e.g. Unity, Visual Studio or any related process.

The reason this happens is that Valve will not release app initialization until every process that mounted its handles has closed. This is the single most common issue we have reported.

### Initialization Status

This indicates the status of the Steam API and will have one of the following values

* Idle\
  This means the API is not, nor has it attempted to initialize. The status will say this anytime the simulation is not running ... that is you must press play for this to work at all.
* Initializing\
  This means the API is trying to initialize, this generally happens very fast so you may never see this.
* Initialized\
  This means the API is initialized and that the values reported are as reported by the API
* Error or Failed\
  This means the API failed to initialize, check your Unity Editor console log for details as to why

### Listed App ID

This is the App ID that appears in the active Steam Settings object. It should match the other listed IDs

### Reported App ID

This is the App ID that Steam API has reported back to us when asked. As far as Steam is concerned this is the App ID you "**are**"

### Steam\_AppId.txt

This is the App ID that is currently recorded in the steam\_appid.txt file

### Inspecting Stats

![](<../../../.gitbook/assets/image (173) (1) (1).png>)

You can use the Stats tab to view and update the value of all registered stats

### Inspecting Achievements

![](<../../../.gitbook/assets/image (179) (1) (1) (1) (1).png>)

You can use the Achievements tab to view and unlock/reset all registered achievements

### Inspecting Leaderboards

![](<../../../.gitbook/assets/image (170) (1) (1) (1) (1).png>)

You can use the Leaderboard's tab to view your score and rank on all registered leaderboards. Leaderboards while one of the simplest aspects of Steam API are also one of the more fragile aspects.

Common issues seen with Leaderboards include

1. You have the sort order set incorrectly
2. You have the leaderboard set to trusted only
3. You made changes in Steam Developer Portal and didn't publish them

We do on occasion see leaderboards "break", this is typically a problem when you change values on the board or delete a board and make a new one with the same name but different settings. In most cases its easiest and best to simply make a new board with a new unique API name.&#x20;

If you need to repair a board that is misbehaving you will need to contact Valve's support as these are backend features Heathen can not see nor effect.

### Inspecting Downloadable Content

![](<../../../.gitbook/assets/image (181) (1) (1) (1).png>)

You can view the subscription status of all DLC in the DLC tab

### Inspecting Inventory

![](<../../../.gitbook/assets/image (164) (1) (1) (1) (1) (1) (1).png>)

The inventory tab will display all the items registered to your game and provides tools for clearing and granting each item

### Inspecting Lobbies

![](<../../../.gitbook/assets/image (185) (1).png>)

The lobbies tab will populate a sub page for each detected lobby and will display the list of members and the lobby's metadata.
