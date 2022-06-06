# 2 User Data

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of [UserData ](../../objects/user-data.md)and displaying common information such as the user's avatar and name.

![](<../../../../.gitbook/assets/image (163) (1) (1) (1) (1) (1) (1).png>)

### What do I learn?

1. That [User Data](../../objects/user-data.md) exists and can be used to display user information
2. How to use [Set User Avatar](../../components/set-user-avatar.md)
3. How to use [Set User Name](../../components/set-user-name.md)
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### Avatar Image

Located at Canvas/Info/Border/AvatarImage

This game object makes use of the [Set User Avatar](../../components/set-user-avatar.md) component to set the local user's avatar image to the UnityEngine.UI.RawImage

### uGUI Steam Name

Located at Canvas/Info/UGUI Steam Name

This game object makes use of [UGUI Set User Name](../../components/set-user-name.md) to set the local user's name to a UnityEngine.UI.Text&#x20;

### TMPro Steam Name

Located at Canvas/Info/TMPro Steam Name

This game object makes use of [TMPro Set User Name](../../components/set-user-name.md) to set the local user's name to a TMPro.TextMeshProUGUI

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as deprecated. They simply drive the buttons in the menu nothing more.
