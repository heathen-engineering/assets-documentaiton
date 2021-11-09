# 3 Stats and Achievements

## Introduction&#x20;

This scene demonstrates the use of Steam stats and Steam achievements.

![](<../../../../.gitbook/assets/image (172).png>)

### What do I learn?

1. Importing Stats and Achievements
2. Using Stats and A
3. How to access the Knowledge Base (where you are now)
4. How to acces the support [Discord ](https://discord.gg/6X3xrRc)
5. How to leave a review 😉

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initalization of the Steam API on start up.

### Avatar Image

Located at Canvas/Info/Border/AvatarImage

This game object makes use of the [Set User Avatar](../../components/set-user-avatar.md) componenet to set the local user's avatar image to the UnityEngine.UI.RawImage

### uGUI Steam Name

Located at Canvas/Info/UGUI Steam Name

This game object makes use of [UGUI Set User Name](../../components/set-user-name.md) to set the local user's name to a UnityEngine.UI.Text&#x20;

### TMPro Steam Name

Located at Canvas/Info/TMPro Steam Name

This game object makes use of [TMPro Set User Name](../../components/set-user-name.md) to set the local user's name to a TMPro.TextMeshProUGUI

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as depricated. They simply drive the buttons in the menu nothing more.
