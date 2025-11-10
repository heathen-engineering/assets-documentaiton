# Build Testing

Steamworks integration requires a correct setup of your game build and environment. This guide explains how to properly test your game, whether locally or through the Steam client, and addresses common pitfalls like crash-on-launch issues or unexpected behaviour.

## Steam Dependency

A typical Steam-integrated game **requires the Steam client** to be installed, running, and logged in with a user who has access to the game's **App ID**. Without this, the Steamworks API will not initialise properly, leading to crashes or other unexpected behaviours.

### Local Testing vs. Steam-Client Testing

**✅ Dev Testing (Local Builds)**

To test your build outside of Steam (e.g. before uploading via SteamCMD), you must place a `steam_appid.txt` file in the root of your game’s directory. This file should contain **only your App ID** as plain text.

* For Unity or Unreal Engine builds, place `steam_appid.txt` next to the executable.
* This allows the Steam API to initialise even if the game is launched from Explorer, terminal, or another non-Steam launcher.

> 📝 Example:\
> `steam_appid.txt`\
> Contents: `123456`

**✅ Build Testing via Steam (Recommended)**

For proper integration and testing:

* Use **SteamCMD** (available in the Steamworks SDK) to upload your build to Steam.
* Set up **beta branches** to separate dev/testing builds from public ones.
* Add **internal testers** via the Steamworks dashboard.

This mimics the live environment closely and is ideal for identifying deployment issues before release.

***

## Common Pitfalls & Fixes

**❌ Game Crashes on Launch**

**Cause:** You’re running a local build without a `steam_appid.txt`, or it contains the wrong ID.\
**Fix:** Add `steam_appid.txt` with the correct App ID. If you’re using App ID 480 (`Spacewar`), be aware it's not suitable for production use.

**❌ Game Tries to Download&#x20;**_**Spacewar**_

**Cause:** You’re using App ID 480 (Valve's sample game) without a valid deployment.\
**Fix:** Replace with your game’s actual App ID and set up the `steam_appid.txt`.

**❌ Steam Relaunches the Game Automatically**

**Cause:** Steam detected the game wasn’t launched via the client.\
**Fix:** This is intentional behavior (`RestartAppIfNecessary`). Use `steam_appid.txt` during dev testing or launch from the Steam client directly.

***

### Special Notes for Unreal Developers

Unreal Engine adds extra integration steps:

* Even if you're **not** using `OnlineSubsystemSteam`, you **must still configure it**. Epic defines required Steam config keys under that system.
* Make sure your `.ini` files are set up correctly (`DefaultEngine.ini`, etc.).
* In the Editor, Steam is often auto-handled, but for packaged builds, all config and `steam_appid.txt` must be present and correct.

Read the [**UE Configure Guide**](configuration/unreal-configuration.md) thoroughly before packaging builds.

***

## Internal Testing Setup

To test builds on Steam:

* Set up a **beta branch** or private test branch via the Steamworks backend.
* Add your testers via the "Manage Users & Partners" section.
* Ensure testers are logged into Steam with appropriate permissions.

| Action                   | Required Setup                                                                    |
| ------------------------ | --------------------------------------------------------------------------------- |
| Local testing            | `steam_appid.txt` in game root                                                    |
| Steam testing            | Upload via SteamCMD, assign App ID                                                |
| Avoid crashes / relaunch | Use the correct App ID and include `steam_appid.txt` When not launching via Steam |
| Unreal builds            | Ensure `.ini` configs are correct even if not using OnlineSubsystemSteam          |

***

**Always test your final build in the same environment your players will use**—via Steam. Catch issues early, avoid negative reviews due to startup crashes, and make use of Steam’s testing tools to ensure a smooth launch.
