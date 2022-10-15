---
description: Bringing friends together
---

# Party / Group Lobby

<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

Steam lobby can be used for a lot more than just matchmaking. In this part of the sample scene we demonstrate using a Steam lobby as a "party" or "group".

<figure><img src="../../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Features

#### Invite Friends

You can invite your friends quickly and easily by pressing the + button on an empty slot. The invite system supports selecting a friend from your friend list or typing in the friends "code" to invite them that way. The same UI features show you your own code so you can share it with friends over other channels such as Discord if you like.

#### Ready Check

You can see when your friends are "ready" to play via a simple Thumbs up or Clock icon on the lower left of their slot. You set your self as "read" or "waiting" using a simple button press.

#### Owner Flag

See who the owner of the lobby currently is, this shows a star of the owners portrait.

#### Leave

You can leave the lobby any time by clicking leave.

#### Chat

You can chat with members of the lobby using simple text messages.

## User Interface

At the top left of the screen is our Party UI. The local user's avatar is always shown in the left most slot with party members listed in the 3 smaller slots.&#x20;

### Invite Tools

Clicking on an empty slot (represented with a + icon) the Invite tool will display

<figure><img src="../../../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

From the invite tool you can select an online friend to invite from a drop down list

<figure><img src="../../../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Or you can type in your friends "code" to invite them manually ... note your code is displayed under your name ... you can select and copy and paste this into whatever social chat you like.

<figure><img src="../../../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

### Ready Check

The party system also demonstrates the built in "ready check" feature of Heathen's Lobby tool. A player can click the Set Ready button to mark them selves as ready or the Set Wait to mark them selves as not ready. The UI will update the thumbs up icon or a grey clock to indicate which users are or are not ready.

### Chat

Below the user icons is the chat window...

<figure><img src="../../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Using the Lobby Chat Director we have implemented a simple chat system that displays the chatting user's name and icon but in a compact way.
