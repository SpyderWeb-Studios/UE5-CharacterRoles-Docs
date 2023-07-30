# Character Register Component

The main aim with this class was to provide an easy way to assign a role to ANY actor that may need it. We didn't want to limit usage to just a player controller or pawn, when we could not know the requirements of every team out there. This Component marks it's Owning Actor as something that requires a Role assigned to it.

The main responsibilites of this class are:
- Registering with the [`CharacterRoleManagerComponent`](CharacterRoleManagerComponent.md)
- Spawning the Assigned [`CharacterRoleComponent`](CharacterRoleComponent.md)

## Setup

Simply attach this component to the actor that can be assigned a role, and have the owning actor implement the [`ICharacterRoleManagementInterface`](../Interfaces/ICharacterRoleManagementInterface.md). This interface's main point is to allow you to define which [`CharacterRoleManagerComponent`](CharacterRoleManagerComponent.md) to use to register (in case you have multiple or have it on anything other than the Game Mode). If the Owning Actor does not implement this interface, then ensure that the[`CharacterRegisterComponent`](CharacterRegisterComponent.md) is on the Game Mode as this component will automatically try to register itself with that actor by default. If this fails, then the product will not crash but instead you'll get an error saying what is going wrong. Please follow the directions in the error to fix it. 

If you are still unsure on how to get setup, please refer to the BP_RoleTest in the Tests folder for reference. If all else fails, please email us at spyderwebstudiosltd@gmail.com with details on your issue. 

## Assignment

You can assign the roles manually if you don't want to use the built in features. It simply needs a Subclass of the [`CharacterRoleComponent`](CharacterRoleComponent.md).

```c++

	UFUNCTION(BlueprintAuthorityOnly, BlueprintCallable, Category = "Character Role")
	bool AssignRole(TSubclassOf<UCharacterRoleComponent> NewCharacterRole);
```

This function will handle the creation, registering and instancing of the component. You'll be able to see it in the editor view after it has been called.

It will also handle the clearing of roles, if you pass in a nullptr or invalid class then it will destroy the current role.