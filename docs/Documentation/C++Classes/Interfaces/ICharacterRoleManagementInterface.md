# ICharacterRoleManagementInterface

This interface was designed to allow our users to define where the [`CharacterRoleManagerComponent`](../Components/CharacterRoleManagerComponent.md) would be stored and not be boxed in by our design choices. It's designed to allow you to be flexible with your implementation. 

It has 3 main functions: 
```c++
	/**
	 * @brief Registers a CharacterRoleComponent
	 * @param CharacterRegisterComponent The CharacterRoleComponent to register
	 * @return True if the CharacterRoleComponent was registered successfully, false otherwise
	 */
	UFUNCTION(BlueprintAuthorityOnly, BlueprintCallable, BlueprintNativeEvent, Category="Character Role Management")
	bool RegisterCharacterComponent(UCharacterRegisterComponent* CharacterRegisterComponent);

	/**
	 * @brief Unregisters a CharacterRoleComponent
	 * @param CharacterRegisterComponent The CharacterRoleComponent to unregister
	 * @return True if the CharacterRoleComponent was unregistered successfully, false otherwise
	 */
	UFUNCTION(BlueprintAuthorityOnly, BlueprintCallable, BlueprintNativeEvent, Category="Character Role Management")
	bool UnregisterCharacterComponent(UCharacterRegisterComponent* CharacterRegisterComponent);

	/**
	 * @brief Retrieves the CharacterRoleManagerComponent
	 * @return The CharacterRoleManagerComponent
	 */
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent, Category="Character Role Management")
	UCharacterRoleManagerComponent* GetCharacterManager();
```

It is mainly used by the [`CharacterRegisterComponent`](../Components/CharacterRegisterComponent.md) to communicate with the [`CharacterRoleManagerComponent`](../Components/CharacterRoleManagerComponent.md) and if you have placed the latter ([`CharacterRoleManagerComponent`](../Components/CharacterRoleManagerComponent.md)) anywhere other than the Game Mode, then you will need to define these functions on any actor that owns a [`CharacterRegisterComponent`](../Components/CharacterRegisterComponent.md) to redirect it towards the correct component.