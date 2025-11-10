# Dialogue Widgets

{% hint style="success" %}
**Note: These tools are in preview**\
We follow a “dogfood” development approach—these tools are actively used and developed within our current WIP games. They are mature enough to share with our GitHub and Patreon supporters, so their documentation is provided here for early adopters.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

A Widget type derived from Dialogue Widget Base, created in Blueprint or C++ is required by the Dialogue Component and will be instantiated when the Open Conversation function is called. This is just a standard Widget with a couple of useful features built in.

When the widget is instantiated, it will link itself back to the owning Dialogue Component meaning the two parts will manage each other's updates automatically so there is no need for you to create logic between them.

## Event Graph

### Update Dialogue Text

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

When the underlying Dialogue Component calls Add Node, if that results in a Type "Update" the Widget's Update Dialogue Text event will be called. So this is where you would set text fields, populate options, and trigger any display/transition animations you might want.

### Option Selection

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

When an option is selected, this is usually a matter of a button press, you want to call Update Selected Option, providing the index that was passed in to you on the Update Dialogue Text event and the index of the option that was selected. This will call back into the Dialogue Component, notifying it of the option selected. It will record that option and progress to the next node, thus invoking Update Dialogue Text again with the next steps text.
