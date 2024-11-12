---
description: A good User eXperience (UX) is everything
---

# System Dialog

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This is a UI element in your game that can be used to reliably display system messages to the end user. While it is typically called a "Error Dialog" or similar it can be used for any sort of "system message" you want to display to the end user separate from your game.

## How To

### Requirements

So we want this dialog to always appear above all other forms of UI and to be a modal dialog ... that is we want to force the user to interact with this before interacting with anything else. We only use this for very important messages that demand user input immediately ... this is a system level dialog.

### Top Most

The easiest way to insure this is always available and always on top is to create it in the Bootstrap Scene in its own canvas that is set to Screen and sorted to render above everything else.

<figure><img src="../../../.gitbook/assets/image (98) (1).png" alt=""><figcaption></figcaption></figure>

### Modal

The easiest way to insure this blocks access to all other UI is simply to fill the canvas with an image that is set to be a Raycast Target. It can be handy to set this image to a dark transparent colour so that it subdues the rendering behind it.

<figure><img src="../../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

### All the Rest

The rest is up to you and would depend on what it is you want and need. For example you will defently need some means to display the message to them. You can use a simple text field but do think about the user experience ... text fields cannot be selected ... InputFields however can. So if you used an InputField and marked it read only they couldn't change its value but they could select it and copy paste.

Follows are some things to consider when setting up your System Message Dialog

* A means to capture screen\
  This should probably hide the System Dialog while taking the screen cap. Our [UX Complete asset](../../../toolkit-for-ui-and-ux/unity/api/screenshot.md) has tools that can help with all of this.
* A means to send you a report\
  This should gather system data and formulate it in a meaningful way and then help them send that data to you either by email, Unity reporting or some other feedback tools like Zendesk ... and you guessed it Heathen has [a tool to help you with that](../../../toolkit-for-ui-and-ux/unity/learning/core-concepts/feedback-tools.md).
* A means to recover\
  Some events will be fatal, others less so. You should give your user a means to return to menu if that is an option or close the app nicely. This can be a simple set of buttons for them to choose from.
