---
description: Building and deploying to a server OS
---

# 👷 Builds

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
With Heathen's Steamworks Complete, there is no special code you need to write for your server build.&#x20;



Heathen's assets use Unity's standard script to conditionally compile for server vs. client builds. That is when you change your build target to a Dedicated Server build our code will compile the appropriate Steam Game Server interfaces and use them in place of client interfaces.
{% endhint %}

Once you have your build you should be able to run it on your local workstation, Don't forget to put a steam\_appid.txt in the root of the build next to the executable. Assuming you have configured the server settings correctly and are initializing correctly you will see output in the console describing the initialization and finally the logon of your Steam Game Server. Migrating this to a server operating system requires a few more steps.

## Dependencies

{% hint style="info" %}
Original notes from [Facepunch Steam Wiki](https://wiki.facepunch.com/steamworks/Server\_Library).
{% endhint %}

You will need to grab the following .dll for your build

* steam\_api64.dll
* steamclient64.dll
* tier0\_s64.dll
* vstdlib\_s64.dll

If you are shipping your server build or using Steam CMD you can include App ID 1007 "Steamworks SDK Redist" in the depot and theoretically, that should bring in the proper dependencies based on platform.

Alternatively, you can use Steam CMD to pull these down locally to a specified install directory.&#x20;

### Where to find them?

You can use SteamCMD to grab them using the Steamworks SDK Redist app.

To do so simply create a text file with some commands in it that we will pass over to Steam CMD to run.&#x20;

In the example below replace the `<platform>` with `windows` or `linux` depending on what target platform you downloading for. Finally, replace `<directory` with the relative path you would like the results to be installed to e.g. `../sdk_files` would put the results in a file next to the context in a folder named sdk\_files.

```batch
@ShutdownOnFailedCommand 1
@NoPromptForPassword 1
@sSteamCmdForcePlatformType <platform>
login anonymous
force_install_dir <directory>
app_update 1007 validate
quit
```

To run the files you can open a command line or create yet another bat file with the following command. Replace the `<sdk_script>` with the relative path for your bat file.

```batch
"SteamCmd.exe" +runscript <sdk_script>
```

<details>

<summary>Windows Example</summary>

#### sdk\_script.txt

```batch
@ShutdownOnFailedCommand 1
@NoPromptForPassword 1
@sSteamCmdForcePlatformType windows
login anonymous
force_install_dir ../sdk_files
app_update 1007 validate
quit
```

#### command

```batch
"SteamCmd.exe" +runscript ../sdk_script.txt
```

</details>

<details>

<summary>Linux Example</summary>

#### sdk\_script.txt

```batch
@ShutdownOnFailedCommand 1
@NoPromptForPassword 1
@sSteamCmdForcePlatformType linux
login anonymous
force_install_dir ../sdk_files
app_update 1007 validate
quit
```

#### command

```batch
"SteamCmd.exe" +runscript ../sdk_script.txt
```

</details>
