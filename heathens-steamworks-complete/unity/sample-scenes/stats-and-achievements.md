# Stats and Achievements

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

<figure><img src="../../../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

The Simple Achievements scene demonstrates reading and updating achievements using the AchievementObject. In this scene we use SetAchievementIcon, SetAchievementName and SetAchievementDescription components to populate the UI showing the icon, name and description of each achievement.

## Configuration

### Set Achievement Icon

Used on the RawImage to load the icon and update it based on changes to the achievement's state such as lock or unlock.

### Set Achievement Name

Used on the TextMesh Pro label to set the name of the achievement.

### Set Achievement Description

Used on the TextMesage Pro label to set the description on the achievement.

## Setting Value

Each of the UI elements shown on the screen is actually a Unity UI Toggle, when clicked it will set the value of the IsAchieved on the [AchievementObject ](../scriptable-objects/achievement-object.md)locking or unlocking it.

Note in this sample scene we do not call Store to commit the change so the changes wont commit until the app is closed. If you wanted to commit the changes before that you can call the Store method on any [AchievementObject ](../scriptable-objects/achievement-object.md)or StatObject to commit the changes now and this will cause the "popup" from Steam overlay to show if applicable.&#x20;

Steam Overlay doesn't work nicely in Unity Editor so we do not demonstrate that here.

### What About Stats?

They work much the same way with regards to setting the value, read the documentation on&#x20;

[Int Stat](../scriptable-objects/int-stat.md)

[Float Stat](../scriptable-objects/float-stat.md)

and [Average Rate Stat](../scriptable-objects/avg-rate-stat.md)

to learn more.

Stats do not have icons so there is no icon to load and each type of stat has its own "data type" but otherwise the process is the same, set the Value of the stat and when ready call Store to commit the changes to the backend.

## Testing

Assuming you are using an unmodified version of the sample scene and Steam Settings you will see messages appear in the Unity Editor Console log detailing each step of the initialization process.

<figure><img src="../../../.gitbook/assets/image (15) (1).png" alt=""><figcaption><p>Example initialization messages</p></figcaption></figure>

In the event of an error details will be listed here along with troubleshooting guidance. In the event you require support please select the first error message in the log and press \[Ctrl + C] this will copy the full message and its stack trace to your clipboard. You can then paste that error into [Discord chat](https://discord.gg/eVVgM36) for live support or into a support email or similar.

Aside from the console output you can click the achievement to toggle it from achieved to locked. You can confirm the value is committed by stopping and restarting the simulation to see that the values retain the last applied state.
