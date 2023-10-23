---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# Unreal Achievements

## Blueprints

### Read Achievement

Below we show getting the achievement, breaking the result down and using it to print a string to the screen including the Achievements friendly name&#x20;

<figure><img src="../../.gitbook/assets/image (363).png" alt=""><figcaption></figcaption></figure>

### Set (unlock) Achievement

Simply unlock/achieve the achievement

<figure><img src="../../.gitbook/assets/image (364).png" alt=""><figcaption></figcaption></figure>

### Clear (reset) Achievement

Simply reset/clear/re-lock the achievement

<figure><img src="../../.gitbook/assets/image (365).png" alt=""><figcaption></figcaption></figure>

## C++

### Read Achievement

Assuming that `apiName` is defined as `FString apiName`.

```cpp
//Get the unlock state and time
bool achieved;
uint32 unixTime;
SteamUserStats()->GetAchievementAndUnlockTime(StringCast<ANSICHAR>(*apiName).Get(), &achieved, &unixTime);

//Optionally get the percentage complete if relevant
float pert;
SteamUserStats()->GetAchievementAchievedPercent(StringCast<ANSICHAR>(*apiName).Get(), &pert);

//Get the Achievement's display name
FString name = FString(SteamUserStats()->GetAchievementDisplayAttribute(StringCast<ANSICHAR>(*apiName).Get(), "name"));
//Get the Achievement's description
FString desc = FString(SteamUserStats()->GetAchievementDisplayAttribute(StringCast<ANSICHAR>(*apiName).Get(), "desc"));
// Get the Achievement's hidden status
const char* DisplayAttribute = SteamUserStats()->GetAchievementDisplayAttribute(StringCast<ANSICHAR>(*apiName).Get(), "hidden");
//Convert the hidden status string to a bool
bool isHidden = (DisplayAttribute && strcmp(DisplayAttribute, "1") == 0);
//Clean up our buffer for the hidden status attribute
delete[] DisplayAttribute;

// This is just an example of using all the data you just gathered
// It's assuming "status" is something that needs all this data
status.Achieved = achieved;
status.Percent = pert;
status.UnlockTime = FDateTime::FromUnixTimestamp(static_cast<int64>(unixTime));
status.Name = name;
status.Description = desc;
status.IsHidden = isHidden;

```
