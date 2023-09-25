# 🔻 Friend Rich Presence Update

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Called when Rich Presence data has been updated for a user, this can happen automatically when friends in the same game update their rich presence, or after a call to [Steam Request Friend Rich Presence](request-friend-rich-presence.md).

### Steam Id

The ID of the user that this event is in relation to

### App Id

This should always be the ID of the current game

## Nodes

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>The event its self is created when you Bind event</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>One way this event can be triggered, the event may also happen as a result of normal Steam updates</p></figcaption></figure>
