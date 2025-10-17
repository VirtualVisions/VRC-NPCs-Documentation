# VRC-NPC Documentation

# NPC Creation Window

This is the tool used for creating your custom NPCs. It can be found in **Tools > NPCs > Creation Window**

<!-- prettier-ignore -->
| Setting | Description |
| --- | --- |
| NPC Target | The GameObject in your scene that will be turned into an NPC. |
| Animator Controller | The Controller used for animating the NPC. This is provided by default, and can be duplicated at will. In the event of Updates, any customizations to the Animator Controller should be done in a duplicate, or you may risk losing your customizations. |
| Dialogue Prefab | The prefab used for the Dialogue Box. This is provided by default, and should only be switched out if you have already made a custom version. |
| Speed | The movement speed of the NPC. This should match the animation speed for the character's walkcycle. |
| Radius | The full width of the NPC's collider. |
| Height | The full height of the NPC's collider. |
| Angular Speed | The rotation speed of the NPC. This likely should be left as is. |
| Acceleration | The acceleration rate of the NPC. This likely should be left as is. |
| Stopping Distance | The distance in which the NPC takes to come to a full stop. This likely should be left as is. |

## How To:

To create an NPC, open the NPC Creation Window, and assign your scene GameObject to the "NPC Target" field. Assuming no animation customizations, you can simply click Create NPC.

**NOTE:** NPCs will require a "NavMeshSurface" component in your scene. It is recommended that you select "Physics Colliders" under "Use Geometry", and uncheck any layers you do not want the navmesh to use. Then simply hit "Bake" at the bottom.

## Agent Controller:

This NPC will now have an Animator, NavMeshAgent, Agent Locomotion, and Agent Controller script, among others. Many of the values you see here are for debug purposes, though currently two options are only accessible via the AgentController:

<!-- prettier-ignore -->
| Setting | Description |
| --- | --- |
| Target | The transform the NPC will constantly attempt to navigate towards while their "State" is set to "Tracking". |
| Path | The Agent Path component the NPC will walk along while their "State" is set to "Pathing". |

Both of these settings are expected to be expanded out into Directions in a future update. Settings after Path (such as Random Path Index, Path Index, etc) will be moved to the Agent Path component in a future update.

# Directors

Directors are the primary way of controlling your NPC, and are comprised of two components:

-   AgentDirectorUdon - Handles options and VRC compatability,
-   AgentDirector - Stores all of the directions to control your NPC.

## Agent Director Udon

<!-- prettier-ignore -->
| Setting | Description |
| --- | --- |
| Agent | The NPC that will be directed. |
| Trigger Type | How the Director will be activated. |
| | - Interact: OnClick for the GameObject. |
| | - OnPlayerEnter: When a player Enters a collider trigger. |
| | - OnPlayerExit: When a player Exits a collider trigger. |
| | - OnLocalPlayerEnter: When the local player Enters a collider trigger. |
| | - OnLocalPlayerExit: When the local player Exits a collider trigger. |
| | - OnAgentEnter: When the Target Agent enters the trigger. |
| | - OnAgentExit: When the Target Agent exits the trigger. |
| | - OnCall: Only when "\_Trigger()" is called on this Director from another script/director. |
| | - OnStart: During the Start event. |
| | - OnEnable: During the Enable event. |
| Retriggerable | If the Director can be used more than once. |
| Use Previous State On Complete | Whether or not to use the agent's previous state when completing the Director. |
| Agent State On Complete | If "Use Previous State On Complete" is enabled, this will choose which state to put the Agent into. |

## Agent Director

This contains a list of all directions to be executed in order.
All directions have a dropdown to select which type of direction will be executed.

### Direction - Wait

A basic delay between directions.

<!-- prettier-ignore -->
| Setting | Description |
|---|---|
| Exit Time | How long in seconds until the next direction will be executed. |

#### Direction - Set Destination

Tell the NPC to navigate towards a destination. Exit Time is elapsed time _after_ the NPC has arrived at this destination.

<!-- prettier-ignore -->
| Setting | Description |
|---|---|
| Target | The transform the NPC will navigate towards. |
| Teleport When Not Visible | Whether the NPC should teleport to it's destination when not being viewed. |
| Exit Time | How long in seconds until the next direction will be executed. |

#### Direction - Teleport To

Immediately teleport the NPC to a destination

<!-- prettier-ignore -->
| Setting | Description |
|---|---|
| Target | The transform the NPC will teleport to. |
| Exit Time | How long in seconds until the next direction will be executed. |

#### Direction - Send Event

Send an Event to an UdonSharpBehaviour in your scene.

<!-- prettier-ignore -->
| Setting | Description |
|---|---|
| Target | The script that shall receive the event. |
| Event Name | The name of the event that shall be run. |
| Exit Time | How long in seconds until the next direction will be executed. |

#### Direction - Dialogue

A comprehensive dialogue interaction with the NPC. Sequential lines of dialogue should be handled with multiple Dialogue directions.

<!-- prettier-ignore -->
| Setting | Description |
|---|---|
| Name | The name displayed in the dialogue text box, labelling the current speaker. |
| Text | The full text that will be displayed in the current box. |
| Audio Type | Which mode should be used for audio playback. |
| | - Typewriter: Play the audio clip once per displayed character, ignoring spaces. |
| | - Voiced: Play the audio clip at the start of the dialogue, intended for fully voiced interaction. |
| Audio Clip | The clip used for the sound playback. For Typewriter, if none is provided, the Dialgoue Box will fall back to it's preset Typewriter clip. For Voiced, if none is provided, no audio will play. |
| Answers | Multiple choice answers to the current dialogue. If none are provided, clicking the dialogue box will progress. Otherwise, an answer must be clicked. |
| | - Option: The text displaying the current answer. |
| | - Director: The director to swap to if this answer is chosen. Useful for having different behaviour for different answers. |

#### Direction - Emote

Immediately teleport the NPC to a destination

<!-- prettier-ignore -->
| Setting | Description |
|---|---|
| Emote Index | The index of the emote you want to play. This is decided via the animator you are using, or the title of the emote as placed in the NPC Override Controller. |
| Exit Time | How long in seconds until the next direction will be executed. |

# Demos

A set of demos have been provided within the pack. "Playground" contains an assortment of features and systems, while "Fetch Quest" showcases the Director system interfacing with a very basic script to fulfill a simple quest system.
