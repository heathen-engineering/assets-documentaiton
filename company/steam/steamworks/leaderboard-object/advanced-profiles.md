---
description: Public rich profiles available all the time
---

# 🗣 Advanced Profiles

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../">Guides and Tutorials</a></td><td><a href="../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../assets/physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../assets/ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

Rich public user profiles can be significant to social games

![Example of a Dota2 user profile from a random google image](<../../../../.gitbook/assets/image (164) (1) (1) (1) (1) (1).png>)

To be effective these profiles need to always be available any time a player sees another players name so as an offline friend, as an entry in a leaderboard, as a team mate in a match, as an opponent that stomped you in a match, etc. The profile needs to always be accessible to every user that might see it without needing to be a friend or actively in a lobby or server with that player.

This means that you cant depend on Steam's rich presence alone though that can be of use, notice the Main Menu text under that user's name. That is from Steam's rich presence but would only list for people who are you or are your friend.

All of the reset of that data is stored in a profile object, this being DOTA its likely stored on the account after all DOTA has access to so much more than we as regular steam developers do. That said we can do nearly the same using Leaderboards to house profile data.

## What is this?

In summary the idea is to create a publicly accessible rich account profile like you would see with DOTA and similar games where user’s can show off there in game accomplishments, favourite builds, top stats and more.

Leaderboards are used since anyone can query a leaderboard and fetch the data contained in it. Leaderboards can be easily written by anyone and can contain more than just a score and rank. The key to this use case is the use of leaderboard details array and leaderboard attachments.

## How To?

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/api/leaderboards" %}
The leaderboard interface
{% endembed %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/leaderboard-object" %}
The leaderboard object its self
{% endembed %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/leaderboard-entry" %}
The leaderboard entry which represents entries on a board
{% endembed %}

Your first step is always to decide what data you want the users to store on/in their public profiles. You will also need to create a serializable struct or object that can house that information.&#x20;

Example serializable

```csharp
[Serializable]
public struct ProfileDataObject
{
    public int level,
    public GameMode favoriteMode;
    public CharacterChoice favoriteCharacter1;
    public CharacterChoice favoriteCharacter2;
    public CharacterChoice favoriteCharacter3;
    public CSteamID clanID;
}
```

As much as is possible try to pack that information into an int\[] with 64 or fewer entries. Of course if your values are already ints then this is very easy, for example the level value in ProfielDataObject above would be a good candidate as would the GameMode assuming it was an enum. Enums are really just ints with names.



Booleans are something we use a lot as game developers and an int can represent 32 of them quite easily. Below I show a bit on how you might pack up to 32 Booleans in a single int&#x20;

{% hint style="info" %}
Yes you can use bit wise operations to do this and yes it is less code to use bitwise and arguably faster operations to execute but bitwise operations tend to make some peoples head smoke and really if your doing this so often that the performance impact is an issue then you should really be cashing profile results.



.NET gives use a more scripter friendly way to monkey with bits that not many seem to know about so I will show that here. You can read more about BitArray here

[https://docs.microsoft.com/en-us/dotnet/api/system.collections.bitarray?view=net-5.0](https://docs.microsoft.com/en-us/dotnet/api/system.collections.bitarray?view=net-5.0)



You can read more about bitwise operations here

[https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators)
{% endhint %}

```csharp
int[] details = new int[3];
details[0] = 42;
details[1] = 1024;

BitArray bits = new BitArray(32);

// bits now represents 32 booleans and is the size of 1 int
// you can set the bits as you would any other array
bits[0] = true;
bits[1] = true;
bits[2] = true;
bits[3] = true;
//etc

//When your ready to turn it back into an int
bits.CopyTo(details, 2);

//The value of index 2 (where we set the bit array) is now 15
// an int set to a value of 15 is [11100000 00000000]

//To turn an int back into a bit array

bits = new BitArray(new int[]{ details[2] });
```

### Why an int array?

Leaderboards store “details” per entry as an int\[] with up to 64 entries. This is fast to read and doesn’t require any serialization so less error prone. You can get clever with this and pack all sorts of data into an int array … for example you can think of an int as 32 Booleans for example but what you do with it is up to you.

### Why a serializable object?

Leaderboards can have 1 attachment per user, this attachment can honestly be any file compatible with Remote Storage but we have already built tools to help you save and load serializable types as files so best to use that.

Our system will use JsonUtility to serialize the file and convert it to byte\[] for storage on Steam Remote Storage, we will then mark the file as shared and attach it to the leaderboard entry for you. Once attached it will be available to people reading the board even if the original is removed from remote storage … or so Valve says.

### How to set the profile?

Lets assume you have defined a leaderboard that will be used as your player\_profles and you have linked it with your game as you would any other leaderboard.

To save a user’s profile you need only create the serializable object and set up the detail array you wish to store and then call upload with a score different than the current score … for ease what we do is alternative between 1 and 0 e.g. if the current score is 1 we force update to 0 if its 0 we force update to 1. You could also increment the score where score represents a “version” number if you like; that is up to you.

```csharp
player_profile.UploadScore(
        0, 
        details, 
        ELeaderboardUploadScoreMethod.k_ELeaderboardUploadScoreMethodForceUpdate, 
        (uploadResult, uploadError) =>
        {
                if(!uploadError)
                        player_profile.AttachUGC(
                                "gamename.profile",
                                myProfileObject,
                                Encoding.UTF8,
                                (attachResult, attachError) =>
                                {
                                        if(attachError)
                                                //Steam said no to attaching
                                });
                else
                        //Steam said no to uploading check why
        });
```

Yes I use a lot of expression there; here is what's happening

1. We simply upload our score and details with a ForceUpdate upload method
2. When that completes we attach our profile data `myProfileObject` and name it "gamename.profile" you really could name it anything or if you wanted to be extra safe makes it name the string value of a GUID. Those are assured to be unique and the name really doesn't matter for a human.
3. When that completes we check for error but otherwise are done

### How to read the profile?

Now that it’s a leaderboard you can do all sorts of very cool things depending on what you stored as score. For now though lets assume you just want to fetch a profile for a specific user

```csharp
UserData[] users = //The users we want to get profiles for

API.Leaderboards.Client.DownloadEntries(
    player_profiles, 
    users, 
    HandleProfiles);
    
// ...

private void HandleProfiles(LeaderboardEntry[] results, bool error)
{
    if(!error)
    {
        foreach(var entry in results)
        {
            entry.GetAttachedUgc<ProfileDataObject>(
                (attachment, attachmentError) =>
                {
                    if(!attachmentError)
                        //attachment is the profile
                });
        }
    }
}
```

The callback will contain the entries for each of the users in your users list. You can use the LeaderboardEntry object to read the details and fetch the attachment e.g.

The callback will contain a populated ProfileDataType assuming there is a valid JSON attachment else it will return the default so null for classes or new for structs.

