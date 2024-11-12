# Cursor System Scene

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (188) (1).png>)

This scene demonstrates the use of animated and context sinsative cursors. Each box changes the style of the defualt cursor and has several controls which will change the context of the cursor several of which are animated.

### What do I learn?

1. How to configure [Cursor States](../../objects/cursor-state.md)
2. How to use the [Cursor Animator](../../components/cursor-animator.md)
3. How to set the active state
4. How to change the default state
5. How to access the Knowledge Base (where you are now)
6. How to access the support [Discord ](https://discord.gg/6X3xrRc)
7. How to leave a review 😉

## Objects

### Managers

This GameObject implaments the Cursor Animator which is responsible for updating the cursors animation.

### Window Style

This GameObject located under the Canvas GameObject implaments the [Mouse Over Cursor State](../../components/mouse-over-cursor-state.md) setting the active state to Win Normal.

### Mac Style

This GameObject located under the Canvas GameObject implaments the [Change Cursor Default State](../../components/change-cursor-default-state.md) setting the default cursor state to Mac Normal on enter and Win Normal on exit.

### Generic Style

This GameObject located under the Canvas GameObject implaments the [Change Cursor Default State](../../components/change-cursor-default-state.md) setting the default cursor state to Generic White on enter and Win Normal on exit.

### Style Controls

In each of the grey boxes represeing a cursor style you will see a number of buttons, input fields, etc. You can mouse over these to see various cursors. The top most button implaments a [Button Cursor State](../../components/button-cursor-state.md) componenet which sets the state to one value on enter and a different value on mouse down. While other controls implament the simpler [Mouse Over Cursor State](../../components/mouse-over-cursor-state.md) which simply changes the state on enter and exit.
