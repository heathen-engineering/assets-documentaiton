# Deploy

So you have built your game and are ready to push it up to Steam, but you are not quite sure how to do this. This article will describe the two main methods for getting your game pushed up to Steam, as well as some of the administrative features around Steam builds and depots as they relate to the topic.

Valve's official documentation on the subject is required reading!

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/sdk/uploading](https://partner.steamgames.com/doc/sdk/uploading)

</details>

## Steam Pipe GUI

This is a standard feature of the Steamworks SDK:\
It replaces the "Steam Build" button in our older versions of Toolkit for Steamworks, as it does exactly the same thing but is authored by Valve. This tool is, in reality just calling the [Steam CMD](deploy.md#steam-cmd) tool for you. We do advise you to read up on [Steam CMD](deploy.md#steam-cmd) in this article to understand what is actually happening.

<figure><img src=".gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure>



You find the SteamPipe GUI tool in the Steamworks SDK zip that you downloaded when you registered as a Steam Developer ...&#x20;

{% hint style="warning" %}
When you definitely did before you started building your game around Steam 😏
{% endhint %}

You can locate this tool in the SDK's tools folder.

<figure><img src=".gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>

## Zip Upload

If your game is small enough, you can upload it as a zip file in the Steam Developer Portal.

<figure><img src=".gitbook/assets/image (275).png" alt=""><figcaption></figcaption></figure>

In short, if the resulting zip file is smaller than 2 GB, you can upload it in the Steam Pipe -> Builds -> Upload Depots option.

## Steam CMD

Steam CMD has a feature "Content Builder" which is the traditional way to upload your games, and in our opinion, the better method. Your first step is to download the Steamworks SDK, which is a zip file that has a slew of tools and examples meant to help you get to terms with the Steamworks tools.

"app build vdf" That app build vdf is just a script that describes what app it is we want to upload for and what depots we want to upload to.

The app builds vdf further references "depot build configuration vdf" files that detail each depot that will be leveraged, and what that depot reads.

{% hint style="info" %}
Are you allergic to using command-line tools?

While we encourage you to learn, as it will open a whole new world of capability for you, there are GUI tools to help you use Steam CMD to upload your builds.

Here is one such example [https://github.com/RPicster/Steam-Upload-GUI](https://github.com/RPicster/Steam-Upload-GUI)\
\
&#xNAN;_&#x54;his tool is not tested, built or supported by Heathen Engineering; it was just the top search result at the time for Steam CMD GUI._
{% endhint %}

{% embed url="https://partner.steamgames.com/downloads/steamworks_sdk.zip" %}
Download the Steamworks SDK
{% endembed %}

Once you have that downloaded, you should unpack it to a location on your local machine. The folder you're looking for within the SDK is the SDK -> Tools -> ContentBuilder folder.

<figure><img src=".gitbook/assets/image (276).png" alt=""><figcaption><p>Shows the ContentBuilder folder within the SDK zip file</p></figcaption></figure>

{% embed url="https://www.youtube.com/watch?v=SoNH-v6aU9Q" %}
A video explaining how this all works
{% endembed %}

In short, you can use a couple of simple commands to upload your build to Steam via Steam CMD. This setup can even be scripted so that all you need to do is run your script.

### Run Build Script

To get started, let us create the script that you will execute to upload your builds. The following is a template you can use.

```
builder\steamcmd.exe +login [Username] [Password] +run_app_build_http ..\scripts\app_build_[appid].vdf +quit
pause
```

To use the above template, open up Notepad or your preferred plain text editor and paste that command in. Next, we are going to replace the following text.

* \[Username]\
  This should be your Steam User Name that you use for the Steam Developer Portal.
* \[Password]\
  This is the password for that same account
* \[appid]\
  This is the numeric app ID that you want to upload

Next, save the file to the ContentBuilder folder ... we suggest you give it a name such as `run_build_MyGameName.bat.` This will make it easier to sort, search and remember which app this goes to.

This script does the following things.

1. Run SteamCmd
2. Log in as the indicated user
3. Indicate the script`..\scripts\app_build_#####.vdf`

The final command there is passing in a file as part of the argument ... a file located in the scripts folder, it's that vdf file that describes what is to be uploaded, where the content should be read from and what depots it should be pushed to.

You can create variations of this script for different builds and different apps. This gives you a 1 click way to upload all your content, and you can even have it upload multiple builds at once.

How?\
The next section covers it.

### VDFs

The .vdf format from Valve does 2 things, there are:

* "appbuild" \
  These VDFs describe what is to be uploaded, e.g. the app id, the description of the build, the content folder the build content can be found in, etc.
* "DepotBuildConfig"\
  These VDFs describe the depot itself that an upload should push to, this will include the depot ID and its file mapping information, as well as any file exclusion rules, such as excluding \*.pdb files from being uploaded

#### Template App Build VDF

This should be saved in the scripts folder with a name such as `app_build_####.vdf,` where the ### is your app ID.

```json
"appbuild"
{
	"appid"	"[appId]"
	"desc" "[description]" // description for this build
	"buildoutput" "..\output\" // build output folder for .log, .csm & .csd files, relative to location of this file
	"contentroot" "..\content\[gameFolder]\" // root content folder, relative to location of this file
	"setlive"	"" // branch to set live after successful build, non if empty
	"preview" "0" // to enable preview builds
	"local"	""	// set to flie path of the local content server 
	
	"depots"
	{
		"[DepotId]" "depot_build_[DepotId].vdf"
	}
}
```

You should replace the text defined below with the values appropriate for your game

* \[appId]\
  The app ID of this build is about
* \[description]\
  The description of this build ... is usually something like "MyGame's base build" or "MyGame's Windows Build"
* \[gameFolder]\
  This is the location of your build content, and as you can see, we assume you're putting your build in the SDK -> Tools -> ContentBuilder -> content folder. We recommend you make sub-folders in that for each game ... and for each platform ... for example
  * sdk/tools/ContentBuilder/content/MyGame/Windows
  * sdk/tools/ContentBuilder/content/MyGame/Linux
  * sdk/tools/ContentBuilder/content/MyOtherGame/Windows
* \[DepotId]\
  This is the list of DepotBuildConfig files to be included, it is an array, so you can include more than 1 for example

```json
"depots"
{
    "123456" "depot_build_123456.vdf",
    "234567" "depot_build_234567.vdf"
}
```

The Depot Build Config define what content they will read or not from the content folder they are pointed to. How this works will make more sense as you read over the template for the Depot Build Configuration

#### Template Depot Build Configuration VDF

This should be saved in the scripts folder with a name such as depot`_build_####.vdf` where the ### is your depot ID.

```json
"DepotBuildConfig"
{
	"DepotID" "[DepotId]"
	"ContentRoot"	"[RootFolderOfTheGame ... where the platform folders live]"

  "FileMapping"
  {
  	// This can be a full path, or a path relative to ContentRoot
    "LocalPath" ".\[Platform]\*"
    
    "DepotPath" "."
    
    "recursive" "1"
  }

  "FileExclusion" "*.pdb"
}
```

Here we will replace the following text

* \[DepotId]\
  This is the depot's ID as seen in the Steam Developer Portal and is a number such as 123456
* \[RootFolderOfTheGame ... where the platform folders live]\
  This is the root folder where the content will be read from ... for example\
  `C:\Builds\ContentBuilder\content\MyGame`
* \[Platform]\
  This is a sub-folder within the content root, so if I entered the value `.\Windows\*` Then I am telling it to read all files and folders in `C:\Builds\ContentBuilder\content\MyGame\Windows`

### Run It

Once you have the 3 layers of scripts created that is the Run Build Script, the App Build VDF and the Depot Build Config VDFs you can now upload your build by simply running the "Run Build Script" you set up.\
\
This can now be easily tied into your build process if your using one or even ran manually by double-clicking the bat file.&#x20;
