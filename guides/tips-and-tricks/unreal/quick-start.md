# Quick Start

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

This article will in-a-nut-shell key features and concepts of the Unreal engine to help developers get a quick understanding of the engine's fundamental features. This is not meant to be a deep dive on anything just a bullet list with notes of things you should understand as an Unreal Developer.

## Game Instance

A class that acts as a manager for the game's global state and persistent data. You can create your own Game Instance by creating a new C++ class or Blueprint derived from GameInstance.

If you use Heathen's Toolkit for Steamworks you would already have similar but derived from SteamGameInstance.

Unlike other objects this object doesn't unload or reload, it is persistent at all times and can be "got" at all times using either `Get Game Instance` or if your using Heathen's Toolkit for Steamworks ... `Get Steam Game Instnace`. this makes it a handy place for global events, error dialogs, system settings, session data that needs to persist over level loads, etc.

As this is a global, starts early and persists thing, its also handy for managing your games subsystems, player inventory for example.

* Always available, part of the game client
* Global State Management
* Persistent Data
* Subsystem Integration
* C++ or Blueprint

## Game Mode

As its name suggests the game defines the nature of a game mode i.e. capture the flag, king of the hill, etc. Every level defines the Game Mode applicable to it and its the Game Mode that is responsible for enforcing the enforcing game rules, selecting player spawning, defines the default classes used for things like the player controller.

See your World Settings in your level to set the current mode and its defaults

<figure><img src="../../../.gitbook/assets/image (457).png" alt=""><figcaption></figcaption></figure>

The Game Mode is the "authority" of the rules the game is running under at the moment and as such is only available on the server. If you a single-player game then your client is also a server, if you're a P2P host e.g. running as a Listen Server ... then you're a server ... but in a traditional Dedicated Server multiplayer game no client will have any access to Game Mode at all.

* Only available on the server
* Defines Default Classes for controllers, pawns etc.
* Handles player spawning rules
* Manages Game State
* Handles Level Transition
* C++ or Blueprint

## Game State

The current state of the game, differs from Game Mode in that this is replicated to all clients. Its generally used to carry info relevant to all clients for example a score, status, etc. as well as providing reference to active Player States.

<figure><img src="../../../.gitbook/assets/image (458).png" alt=""><figcaption></figcaption></figure>

* Always available, but is owned (authority) by the server
* Replicates (syncs) data from the server for the game
* Used to manage server data that all clients should see (score, timers, status, etc)
* Access Player State

## Player State

Stores and replicates data regarding a specific player, this can be thought of as a child or member of the Game State and is owned (authority) by the server as the Game State is. Its generally used to track player-specific data that is replicated to all other users e.g. health, score, name, etc.

{% hint style="info" %}
Do not confuse Player State with Player Controller
{% endhint %}

* Always available (while this player is), but is owned (authority) by the server
* Replicates (syncs) data from the server for this player
* Used to manage player data that all clients should see (score, name, health, etc.)
* Used by Game Mode to manage player-specific rules and states

## HUD

The Game Mode defines a HUD which is a class used to define the "heads-up display" e.g. the UI. In current versions of Unreal its a bit more common to leverage User Widgets for this purpose which we often drive from else where such as using the Common User Widget system to stack widgets driven on player input e.g. often driven from the Player Controller.

## Pawn & Controller

#### Pawn

A type of Actor that can be possessed and thus controlled by a player or AI via the Controller. Pawns are the in-game world representations of players and NPCs.

* Can move around
* Can be "possessed" by a Controller
* For human players this is where we would generally apply the camera and its logic

#### Controller

This object exists to control a pawn and has two main types

* Player Controller\
  This is used for human players and mostly handles the translation of human input into actions to be performed ... this is the main "interface" for a human into he game world
* AI Controller\
  This is used for ... well everything else ... it's the same thing but AI-driven usually via AI Behaviours&#x20;

## Default Pawn Class

An attribute set on the Game Mode via the World Settings defines the pawn class that will be spawned for each player. The Default Player Controller will "possess" the pawns spawned for players and is also defined on the Game Mode via the World Settings.

## Default Player Controller

An attribute set on the Game Mode via the World Settings defines the controller class that will be spawned for each player and will possess the related pawn.

## AI

Unreal has a robust flexible and very powerful toolset for AI. As you learned in the Pawn & Controller section characters are generally defined as Pawns and can be possessed by a Controller. AI Controllers are controllers the AI system drives. While you have many options for setting these up the Behaviour Tree and Blackboard coupled with NavMesh and the Environment Query System is the default "Unreal Way" to go about it.

See the following sections for more details on each

## Behaviour Tree

{% hint style="info" %}
This is not a Finite State Machine, do not treat it like one you will have a bad time if you do
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=hbHqv9ov8IM" %}

Behaviour Trees are simple yet flexible, I strongly sugest you read up on the theory for them as this will help you build simpler, more performant and yet far more effective trees than simply assuming they are similar to other AI node graph editors

[https://dev.epicgames.com/community/learning/courses/67R/unreal-engine-introduction-to-ai-with-blueprints/qzZ2/unreal-engine-behavior-tree-theory](https://dev.epicgames.com/community/learning/courses/67R/unreal-engine-introduction-to-ai-with-blueprints/qzZ2/unreal-engine-behavior-tree-theory)

The link above is of particular use.

Structurally trees are composed of a few key objects

* Root Node\
  The is simply the start of the tree
* Composite Nodes\
  These control the flow of the tree and come in 2 main forms
  * Selector\
    This will run from left to right and will stop when one of the nodes succeeds
  * Sequence\
    This will run left to right stopping when one fails
* Decorator Nodes\
  These can define conditions for the nodes to run such as has a target or not
* Task Nodes\
  These are the actions or behaviours that will be done&#x20;
* Service Nodes\
  These run in the background on a tick and are generally used for a continuous check or simple looping process

## Blackboard

This is a data structure used in conjunction with Behaviour Trees and provides a structured way to store data that can be used between nodes and easily accessed by decorators.

* Standard data storage for a tree
* Members are easily accessible from Nodes
* Useful for decorators and services

## NavMesh

Unreal's Navigation Mesh, fairly common feature of most engines in Unreal's case it has a lot of very useful built-in features including modifiers for shaping the mesh optionally at run time. Filters to help govern how various AI may path across the mesh and well integrated with other features in the AI toolchain.

Modifiers and Filters are key concepts when working with Unreal Nav Mesh. Modifiers do just that, cut holes in the mesh or change its state. Filters adjust how queries on the mesh happen and generally are used to increase or decrease the weight of navigating through a given area.

For example, you can use filters to define roads, rough areas, etc. and thus the AI will be able to walk anywhere but will prefer to walk on the road and around the rough area.

* Easily create an area for navigation
* Modifiers help sculpt the mesh to suit your needs and can be dynamic or static
* Filters help weight the mesh for more fine-tuned pathing

## Environment Query

This is a system that helps your AI make "smarter" decisions. It lets you check an area and assign weights and values to desired positions based on rules you define. These can be used to help your AI choose cover in a firefight, or duck around a corner to break line of sight or choose more favourable areas to set up for an attack.

The system is easily configured and very flexible so a deeper dive is needed to really get a grip but the following are some key points to be aware of

* Query Template\
  Defines the criteria and conditions for the query, composed of one or more test conditions such as distance, visibility, etc.
* Query Instance\
  A specific instance of a query, this is a parameterized expression of a template
* Generator\
  The volume to query, basically a shape such as box, sphere or even a whole Nav Filter
* Score\
  The result of a query is basically a set or grid of options and each of the options or nodes within it are scored via an evaluation based on the conditions of the query template
* Context\
  can consider character state and objectives or be used for environmental changes

## Input Action

Unreal's input system is similar to those seen in other engines and even to Steam's Input. The basic idea is you describe "actions" that your game has and can then define a context for these actions and the related mapping of the actions to inputs such as mouse, keyboard, touch or controller.

You can think of these as "events" that will be called/invoked when the mapping happens e.g. is true.

## Input Mapping Context

A mapping context defines the actions that are available when this context is active, the easiest way to think of this is as a group of actions that can be made available or disabled together as a "context".

Put more simply you "Add" or "Remove" a context from being active and thus enable or disable the events related to it from triggering.

A good example of this would be to have a context for walking, swimming, flying and driving. You can then adjust which is active based on what is happening in the game world and thus modify what events are raised and how and each of these mapping contexts defines its own mapping e.g. the player could be allowed to map different inputs to the same action depending on the mapping.
