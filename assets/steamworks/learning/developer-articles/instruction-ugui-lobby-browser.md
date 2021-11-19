# Instruction: uGUI Lobby Browser

## Introduction

This is a simple walk through for creating your own lobby browser using uGUI.

### Why not give us sample code / scene?

We may eventually but there are 3 different Unity UI frameworks each having multiple ways to accomplish the goal. In our experience when a Unity Developer gets sample code they tend to treat it like production ready product code they can ship on and expect support to match.

Put very bluntly this instruction is meant as instruciton not a product we will be supporting. That may change but for now that is what it is.

## Requirements

### Unity Scripting

You will need a basic understanding of C# scripting in Unity. You will be creating a few componenets aka MonoBehaviours using basic concepts.

### Steamworks Complete

While you can probably apply this to any Steamworks.NET based solution we are writing this from the point of view of Steamworks Complete so if you want to follow along you will need that.

### Unity 2019 LTS or later

At the time of writing 2019 LTS is the primary Unity Asset version so that is what we will use here. 2020 LTS and 2021 LTS should work just as well. Later versions may also work but my crystal ball is hazy on that as they dont exist yet.

## Concept

In this approch we will be using the Leaderboard Manager and its events to update Unity uGUI UI objects based on lobby search results. There are other approches but the concepts discribed here should be applicable to virtually any sort of "Lobby Browser" UI you might want to create.

The following are key componenets we will be using. Some are provided with Steamworks Complete some we will be creating here.

### Lobby Manager

Part of Steamworks Complete, read more about it [here](../../components/lobby-manager.md).

### Verticle Layout

Part of Unity's uGUI UI Framework, read more about it [here](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/script-VerticalLayoutGroup.html).

### LobbyDisplayController

A script we will be creating in this instruction.

## Creating the componenets

The main componenet we need to create is the LobbyDisplayController this controller will be added to a prefab or template that we can instantiate at runtime to populate our lobby list. It will reference the UI fields that display lobby data to the user, such as name and a member count and will provide the logic to join the lobby when the user clicks a button.

### Lobby Display Record

```csharp
#if !DISABLESTEAMWORKS && HE_STEAMCOMPLETE
using UnityEngine;

namespace HeathenEngineering.DEMO
{
    public class LobbyDisplayRecord : MonoBehaviour
    {
        [System.Serializable]
        public class JoinFailedEvent : UnityEngine.Events.UnityEvent<Steamworks.LobbyEnter_t>
        { }

        [SerializeField]
        private TMPro.TextMeshProUGUI nameLable;

        
        public HeathenEngineering.SteamworksIntegration.LobbyDataEvent evtJoinCompleted;
        public JoinFailedEvent evtJoinError;

        private HeathenEngineering.SteamworksIntegration.Lobby lobby;
        public HeathenEngineering.SteamworksIntegration.Lobby Lobby
        {
            get => lobby;
            set
            {
                lobby = value;
                nameLable.text = lobby.Name;
            }
        }

        public void Join()
        {
            HeathenEngineering.SteamworksIntegration.API.Matchmaking.Client.JoinLobby(lobby, (result, error) =>
            {
                if (error)
                    evtJoinError.Invoke(result);
                else
                    evtJoinCompleted.Invoke(lobby);
            });
        }
    }
}
#endif
```

This object will be used by the:

### Example Populated Result List

```csharp
#if !DISABLESTEAMWORKS && HE_STEAMCOMPLETE
using HeathenEngineering.SteamworksIntegration;
using UnityEngine;

namespace HeathenEngineering.DEMO
{
    public class ExamplePopulateResultList : MonoBehaviour
    {
        public GameObject template;
        public Transform layoutRoot;

        public HeathenEngineering.SteamworksIntegration.LobbyDataEvent evtJoinCompleted;
        public LobbyDisplayRecord.JoinFailedEvent evtJoinError;

        public void UpdateDisplayList(Lobby[] lobbies)
        {
            //Get all the old entries
            System.Collections.Generic.List<LobbyDisplayRecord> entries = new System.Collections.Generic.List<LobbyDisplayRecord>();
            layoutRoot.GetComponentsInChildren(entries);

            //Add blank entries to meet the result count
            while (entries.Count < lobbies.Length)
            {
                var GO = Instantiate(template, layoutRoot);
                var entry = GO.GetComponent<LobbyDisplayRecord>();
                
                //Echo the events up to this parent controller
                entry.evtJoinCompleted.AddListener(evtJoinCompleted.Invoke);
                entry.evtJoinError.AddListener(evtJoinError.Invoke);

                //Add the new entry to the list
                entries.Add(entry);
            }

            //Remove exces entries to meet the result count
            while(entries.Count > lobbies.Length)
            {
                var target = entries[0];
                entries.RemoveAt(0);
                Destroy(target.gameObject);
            }

            //Set the entries lobby field to match our lobby results.
            //This will reuse entries if available saving some spawn time
            for (int i = 0; i < lobbies.Length; i++)
            {
                //Set the lobby reference
                entries[i].Lobby = lobbies[i];
            }
        }
    }
}
#endif
```

## Use

With these two objects created you can add the ExamplePopulatedResultList to a a GameObject and reference a template LobbyDispalyRecord and the colleciton to instantiate the records into on it.

The template LobbyDisplayRecord should be a prefab or disabled GameObject that implaments the LobbyDisplayRecord componenet and will be instantiated (cloned) for each lobby found into the provided collection.

The Colleciton in most cases will be a layout component most likely a Vertical Layout component such that all child objects sort them selves automaticaly.
