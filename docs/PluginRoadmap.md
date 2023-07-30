# Plugin Roadmap

This is what we have planned for the future of this plugin. We aim to have a LTS version of this plugin for 5.2, so our customers don't need to worry about being unsupported. 

## Current Features

- Can define Roles using the [`Character Role Component`](Documentation/C++Classes/Components/CharacterRoleComponent.md):
    * Define Win and Lose Conditions
    * Role Names
- Players and Designers can finetune the settings on the [`Character Role Manager Component`](Documentation/C++Classes/Components/CharacterRoleManagerComponent.md) in Editor or Runtime:
    * AssignedRoleCount -> How many of this Role has currently been Assigned (Read Only)
	* RoleCount -> How many of this Role can be Assigned
	* RoleProbability -> How likely is this role to be Assigned (0-1)
	* bCanBeOverwritten -> If the Role can be overwritten by another Role
	* bCanBeMissed -> If the Role can be missed, or if it has to be assigned

- [`Character Register Components`](Documentation/C++Classes/Components/CharacterRegisterComponent.md) automatically create and add the right [`Character Role Component`](Documentation/C++Classes/Components/CharacterRoleComponent.md) to their Owners at runtime, no blueprint required. 


## Future Features

- Integrate Gameplay Ability System into the system to allow different Roles to have different abilities automatically
- Have a Role Priority attribute to the CharacterRole Struct to allow designers and players more control over the Assignment process