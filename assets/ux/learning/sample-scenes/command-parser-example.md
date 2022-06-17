# Command Parser Example

{% hint style="info" %}
Available in UX [Complete](https://prf.hn/l/rpV2JWe)
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (171) (1) (1) (1).png>)

This scene demonstrates the use of the Command System. Command system lets you parse string input such as from an in-game chat and trigger paramiterized [game events](../../../system-core/game-events.md). This system can be used to create console or MMO chat like command systems for player chats, emotes, help systems and more.

### What do I learn?

1. How to use the Command Director
2. Setting up a Command Library and Commands
3. How to use both simple and paramiterized commands
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

## Objects

### Example Scripts

The example scripts GameObject implaments the [Command Director](../../components/command-director.md) component which provides easy access to parsing input and exposes a simple Unity Event which will be raised any time a command is found from input.

This GameObject also implaments a simple custom sample script which simply reads input text from the text box and passes it to the Command Director for parsing. The Command Parser Example Script also handles the Command Found event and simply invokes the event as a crude in-game example.
