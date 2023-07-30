# Character Role Manager Component

This component is in charge of managing the roles, which in more detail means:

* Holding the Role Map, which is where you not only define which [`Character Role Component`](CharacterRoleComponent.md) Subclass to use but also all the data related to each
* Registering and Unregistering [`CharacterRegisterComponents`](CharacterRegisterComponent.md) and verifying that they are valid
* The assignment of [`Character Role Component`](CharacterRoleComponent.md) Subclass to each [`CharacterRegisterComponents`](CharacterRegisterComponent.md)
* Verifying the Win and Lose conditions for each [`Character Role Component`](CharacterRoleComponent.md) and broadcasting if any character has lost or won

This component is designed to be held on the Game Mode, but if you want every player to be able to see every other players roles then we'd recommend putting this on the Game State. 

With this in mind, we have designed it to be run exclusively on the server. Most, if not all, of the functions are Authority Only so are only going to be called if the execution is already with Authority, which is different to a RPC. 


## Setup

Getting the component setup is easy, simply add it the Game Mode or Game State (depending on your requirements). 

Below is an example of how to get prepare the relevant roles within the component, and of course you can determine this at Runtime

![](/assets/Examples/Components/CharacterRoleComponent/Setup.png)

## Registering and Unregistering

We have made a [`ICharacterRoleManagementInterface``](../Interfaces/ICharacterRoleManagementInterface.md) that acts as a integral part of this system. This component implements this to maintain a consistent code base.

This component will only register a Valid [`CharacterRegisterComponent`](CharacterRegisterComponent.md) that hasn't already been registered. Similarly, unregistering will only work on a valid and already registered [`CharacterRegisterComponent`](CharacterRegisterComponent.md).

[`CharacterRegisterComponents`](CharacterRegisterComponent.md) will automatically attempt to register themselves on BeginPlay, which is why in our example we have set up the Role Assignment to occur on the next tick after BeginPlay. We are not currently aware of a way to determine if every Component has registered themselves, but if this changes then we will update this to a more deterministic method. 

## Assignment

This is the main point of this plugin, as we wanted to create something that was easy to use, robust and reliable, but also powerful enough to generate random assignment and allow players to set up there own rules. 

We came up with an algorithm that accomplishes all of these challenges. Depending on the settings, the roles will be assigned based on a per role basis. If a role has been assigned to a [`CharacterRegisterComponent`](CharacterRegisterComponent.md) that cannot be overwritten then that [`CharacterRegisterComponent`](CharacterRegisterComponent.md) will maintain that role. If a role is missable then there is a chance that the role will not be assigned at all. If a role is not missable and all roles currently assigned can not be overwritten then currently this role is skipped, though in our [Plugin Roadmap](/PluginRoadmap) you can see that we are planning on rectifying this. 

When all the roles have been chosen for each [`CharacterRegisterComponent`](CharacterRegisterComponent.md), a final iteration is performed which is where the actual assignment is performed. Please see the [`CharacterRegisterComponent`](CharacterRegisterComponent.md) for further detail, but the short version is that a [`CharacterRoleComponent`](CharacterRoleComponent.md) of the relevant class is created and attached to the owner of the [`CharacterRegisterComponent`](CharacterRegisterComponent.md). 

## Verifying Win and Lose Conditions

These are 2 separate functions, that each check each element in the `RegisteredCharacterRoleComponents` for their respective check. A [`CharacterRoleComponent`](CharacterRoleComponent.md) defines their own Win and Lose Condition functions (that can be implemented in C++ or Blueprint) and all this function does is check if any return true. If any do return true, then it calls OnCharacterRoleWinConditionMet or OnCharacterRoleLoseConditionMet respectively and continues onto the next in the list. This is to make sure that every role that has met their condition gets the correct outcome.  
