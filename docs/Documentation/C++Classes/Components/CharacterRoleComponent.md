# Character Role Component

This is the component that you will use to create your own roles. It is an abstract class, which means that this base class cannot be used directly and is another form of protection. 

You can make this class in either C++ or Blueprint, depending on what you are more comfortable using. We have added an example for both, for you to use as reference.

It has a 2 basic methods, to define the Win and Lose conditions for this role.

```c++
/**
	 * @brief This function defines the win condition for this CharacterRoleComponent
	 * @return True if the win condition was met, false otherwise
	 */
	UFUNCTION(BlueprintAuthorityOnly, BlueprintCallable, Category = "Character Role")
	bool WinConditionMet();

	/**
	 * @brief This function defines the lose condition for this CharacterRoleComponent
	 * @return True if the lose condition was met, false otherwise
	 */
	UFUNCTION(BlueprintAuthorityOnly, BlueprintCallable, Category = "Character Role")
	bool LoseConditionMet();
```

![](/assets/Examples/CharacterRoleComponent/WinCondition.png)

![](/assets/Examples/CharacterRoleComponent/LostCondition.png)


There are plans for this component to integrate the Gameplay Ability System. For more information, please refer to the [Plugin Roadmap](/PluginRoadmap).