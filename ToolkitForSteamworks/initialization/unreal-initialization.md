# Unreal Initialization

Unreal will initialise for you by default. The Steamworks SDK integration is a built-in part of the Unreal Engine. Heathen's Toolkit is built on top of that and exposes it to Blueprints for you.

As a result, there are no special steps required to initialise Steamworks when our toolkit is present for an Unreal package (built game).

## PIE (Play in Editor)

Unreal's built-in Steam plugin will not initialise Steamworks when simulating in PIE.&#x20;

Using our tools, however, you can force Steamworks to initialise even in PIE, making it available for dev testing in the editor.

Please note that Steam Networking is not available in PIE. This is a limitation of Unreal Engine; it disables the Steam Sockets drivers when running in PIE.

<figure><img src="../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure>

You can call the Initialise Steam API from anywhere to initialise the API. This is a safe call, that is, if the API is already initialised, it will just return the current state; if it's not, it will initialise and return the result, meaning you can safely set this at the start of any logic you want to run in the editor for testing, and it won't hurt anything even in a build.
