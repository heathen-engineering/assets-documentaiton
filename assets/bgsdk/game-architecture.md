---
description: Understanding how the blockchain fits in with your game's architecture
---

# Game Architecture

## Introduction

Blockchain, NFT, Tokens, there are a lot of buzz words around blockchain technology and a lot of uses for that technology. This article will attempt to demystify some of the concepts and paint a picture of a typical game that leverages blockchain technology.

## Diagrams

### High Level Architecture

![](<../../.gitbook/assets/image (68).png>)

{% embed url="https://sketchboard.me/fCFVXoq2HSV#/" %}

The above diagram shows the basic parts involved with a typical BGSDK enabled game. The upper most portion labelled the "Game World" is a standard arrangement for any game with the only addition being the [BGSDK Model](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#model-or-data-model). The [Model](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#model-or-data-model) is simply a means by which you can link or relate a [blockchain](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#blockchain) artifact ([Token](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#token) or [Contract](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#contract)) to an object in your game such as models, audio, prefabs, etc.‌

Take note of the colours used, these colours will be used in later diagrams to indicate where a process is. For example a red process in a diagram represents a process of the [Game Client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#game-client).

### Handling new users

![](<../../.gitbook/assets/image (69).png>)

In the above diagram we see the Start labelled in red. This represents a new player starting up your [game client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#game-client) and authenticating to your [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#backend-service).‌

Your [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#backend-service) would determine if this is a new player or an existing one. The specifics for that will depend on your [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#backend-service) provider.‌

If the player is decided to be new, it is typical that you would create the required [white label wallets](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#white-label-wallet) for the player, and associate the [wallet](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#wallet) ID or IDs with the player's account in your [backend system](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#backend-service).‌

If the player is an existing player, you would want to query the list of [tokens](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#token) in that [wallet](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#wallet), and notify your [game server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#game-server) of the contents. That is you read the "inventory" of the [wallet](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#wallet) and notify the [game server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#game-server), or [game client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0US8BRvMoxjxPDoIz/assets/bgsdk/game-architecture#game-client) of that content so it can use it in gameplay.

### Linking wallets to users

![](<../../.gitbook/assets/image (70).png>)

Carrying on from the above diagram [Handling New Users](game-architecture.md#handling-new-users), this diagram shows the [backend service](game-architecture.md#backend-service) calling the Venly Web API to create a new [White Label Wallet](game-architecture.md#white-label-wallet). This process creates a [wallet ](game-architecture.md#wallet)with a given "wallet id". A wallet id is simply a unique string you can use as a key between your user data and Venly wallets.

Its up to you and your [backend service](game-architecture.md#backend-service) to then associate this wallet id with your player's account and or a given character.&#x20;

### Minting Tokens

In game terms this means "dropping" or "spawning" items for the player that are items that exist on the blockchain.

![](<../../.gitbook/assets/image (71).png>)

Here we see the start as the [Game Client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-client) notifies the [Game Server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-server) that some action was performed. This could be for example the player attacking a boss.‌

The [Game Server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-server) will process that action and may determine for example that said strike killed the boss. The [Game Server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-server) will then notify the [Backend Service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#backend-service) of this boss kill so that the [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#backend-service) can process a loot table and probability matrix, or whatever other process your game may do to determine what if anything resulted.‌

In this example let’s assume that the [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#backend-service) has determined that a reward is due. This is represented by the Green diamond at the top of the graph. The [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#backend-service) will now request the required items be minted by the [Venly Web API](https://docs.venly.io/api/api-products/nft-api/mint-nft). This request will indicate what [wallet](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#wallet) by ID the item should be minted into.‌

Assuming all went well, the user will have a new item. At this point we are at the middle Green diamond in the graph above. The [backend service](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#backend-service) will now notify the [Game Server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-server) of the new inventory item.‌

The [Game Server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-server) will then validate, and assuming it’s a valid known item it will notify the [Game Client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-client).

### Linking Token to GameObject

![](<../../.gitbook/assets/image (72).png>)

The above diagram starts in our example case with the [Game Server](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-server) notifying the [Game Client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-client) of a change in inventory state. This would be, for example, the last step as described in the above diagram where we walked through the process of generating an item.‌

The [client](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#game-client) receiving this notification would look up the related [Token](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/game-architecture#token) by matching the Token ID with the ID defined on the [Token Scriptable Object](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/artifacts#token). Token Scriptable Objects are a feature of the BGSDK Foundation. You can learn more about that in the [Artifacts](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/artifacts#introduction) section of this knowledge base.‌

Assuming a match was found, we now know which object and how many where just granted to this user. You can associate the [BGSDK Scriptable Objects](https://app.gitbook.com/@lodendsg/s/heathen-kb/\~/drafts/-Me0TuLBgO82-XdjPo2j/assets/bgsdk/artifacts) with any other game objects you like, as you would associate any Unity object with any other. For example, you might associate a material representing a skin, or a prefab containing a skinned mesh character or any number of objects relevant for your game.

## Terminology

### Blockchain

This is any number of crypto chain technologies. To keep it simple you can think of this simply as a distributed database. That is a database that exists "in the cloud" to use yet another buzz word. The advantage to this is that data on the chain is accessible from everywhere, not just in your game. It is also not feasible to hack or cheat the chain since everyone can see it and everyone can validate its state. Consequently, it is also not possible to hide data on the chain as again anyone can see it and validate its state.

### NFT or Non Fungible Token

This is simply a type of token where each individual token is uniquely identifiable; in contrast a "fungible" token is a token where any individual specific token is wholly interchangeable with any other token ,e.g. it is not unique unto itself. An older term for this concept is "serialized" or "non-serialized" objects. A common example would be in manufacturing a bolt, screw, etc, the item is a "non-serialized" object. That is there is no relevant difference between any given bolt or screw. An example of a serialized object would be a graphics card, CPU, monitor, etc, each of which has a "serial number" that uniquely identifies that specific instance.‌‌

In the world of game design, a NFT would be something you need or want to uniquely identify such as a piece of armor, a weapon, a character, etc. This contrasts with subjects you do not need to uniquely identify e.g, currency, consumables, reagents, etc.

{% hint style="info" %}
_**Fungible NFT**_

There is no such thing as a Fungible NFT, though this term is thrown around sometimes. the abbreviation NFT stands for "Non-Fungible Token" as such you cannot have a "fungible non-fungible token"

Heathen Engineering will never refer to a "Fungible NFT" however in your exploration of blockchain technologies, communities, etc. you may run across that term and what they really mean is "Fungible Token" or a token whose instances are not uniquely identifiable or relevant, such as a currency.
{% endhint %}

### Token

This may refer to a fungible token when used in a context of NFT vs Token, however more often than not it simply means any token, be it fungible or non-fungible. When using the term in relation to your game's design and structure, Token means a token type. That is the definition of what a "sword" is for example, whereas when you are using the term Token as in the property a user has in its wallet. "I have 10 sword tokens in my wallet" is referring to instances of a token.

### Token Definition

Note in some contexts this may simply be described as "Token" such as "I have 4 Tokens defined in my contract". What this phrase means is that I have defined 4 types of Tokens in a contract e.g, 4 Token Definitions.

Token Definition may also be referred to as "Token Type", "Token Template" or simply as "Token". The general concept though is that it is a definition of a type of token that can be minted on the chain and is described as a member of a given contract.

### Contract

With regards to use in game development, a contract is most simply understood as a collection of Token Definitions. This can be useful for some games where you have multiple regions with differing token definitions. In most cases however, a game is likely to only need 1 contract which will define all token types, aka token definitions.

### Wallet

A wallet is an object on the chain which expresses ownership of tokens, and quantities of tokens owned. In the context of a game, it can be thought of as an "inventory" or "bank" space. There are various types of wallets, each of which are described below.

### White Label Wallet

This is a concept seen in multiple places. With regards to this tool we use the term as used by Venly, i.e a White Label Wallet is a wallet that is owned by the App in question, and is used as the app controlled "inventory" of a given user. In a typical use case, you will generate 1 or more White Label Wallets for a user and associate those wallet IDs with the user's account, or a character on the user's account, etc.‌

By user's account, we mean how your game understands this user as an individual e.g., a login for the user, a PlayFab account, Google account, etc. Your game will need a means to associate the White Label Wallet ID (a simple string) with that user account. The wallet itself is owned by your app, not the user in question.

### Personal Wallet or User Wallet

This term is used in the scope of this tool, and with Venly to refer to a wallet that is not a White Label Wallet or is otherwise the property of an individual, not your app. The term is only meaningful in so far as differentiating a personal wallet from a White Label Wallet, for example; "I need to transfer my items to my Personal Wallet". This means you want to transfer items to a non-white label wallet that you as a person own.

### Backend Service

A common concept in game design, this may also be referred to as your "Live Ops" service or "Operations Service" or occasionally "Platform Service". Some examples of popular backend service providers include:

* [Steam](https://store.steampowered.com)\* (Valve)
* [PlayFab](https://playfab.com) (Microsoft)
* [GameLift](https://aws.amazon.com/gamelift/) (Amazon)
* [GameSparks](https://www.gamesparks.com)
* [Firebase ](https://firebase.google.com)(Google)

{% hint style="info" %}
_**\*Steam as a Backend Service provider**_

While Steam is technically a backend service provider, and that is why we list it here, It does not provide for a Trusted Server and so is not enough for a blockchain enabled game. Steam is often times used in tandem with other Backend Service providers. You can learn more on this subject from our [Steamworks API](../steamworks/)
{% endhint %}

A backend service is going to be key for any game that is blockchain enabled in that you will need a trusted server, and this is a feature often provided for by a backend service provider usually via a feature they would call "Cloud Scripting" or "Web Scripting"‌

Backend Service providers offer a wide array of services including account management, player data storage and management, often including hosting, allocating and managing game servers and much more. Whether or not your game is a "live service" it will probably benefit greatly from having a Backend Service provider as opposed to using a home-grown trusted server, such as a simple self-hosted web server.

### Trusted Server or Trusted Service

This is another common concept to game design and one of particular importance to any blockchain enabled game. The idea is simply that it’s a trusted system e.g. a system you can trust is secure and whose actions are considered safe. This trusted system will be used to perform any action that is deemed sensitive such as authentication, account management, user data management and of course blockchain tasks such as minting, transferring, and burning tokens.‌

The role of Trusted Server/Service is usually filled by a Backend Service provider as one of many features or services they offer. It is possible to host your own trusted server. Put simply a trusted server is usually a simple Web Server that is sufficiently protected from attack and handles any sensitive operations that are not appropriate to be handled by a game server, or certainly not appropriate for a game client.

### Model or Data Model

This refers to the structure of your data, and in the context of these articles it refers specifically to the "model" relevant to blockchain. That is, it refers to the token definitions and how they relate to objects in your game world. Defining the model and providing the Unity objects needed to link the blockchain artifacts with artifacts in your game is the primary function of the BGSDK Foundation.

### Game Client

A common term referring to the program your player is running.&#x20;

{% hint style="danger" %}
You should always assume that the Game Client is compromised. That is, you must assume that the program your player is running and that is talking to your services has been hacked or is not your game at all, rather is something else simulating your game.

As such you should never trust anything the game client says or does.
{% endhint %}

### Game Server

A common term referring to the program running on system you are hosting, acting as the server for the game world.

{% hint style="warning" %}
While the game server can generally be assured to be your program, it is also serving (typically) many users and you must assume that some or all those users are actively exploiting the server. As such you should not trust the server to perform sensitive actions, nor should you store sensitive data on that server or where that server can get at that data without furthermore secured checks.

Game servers are typically trusted to validate gameplay logic e.g, did X user hit Y user for Z points, but are not trusted to perform authentication, account management, payment processing, user data management, or of course processes such as Minting, Transferring or Burning of blockchain assets which themselves represent some real value.
{% endhint %}
