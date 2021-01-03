# Macros
There exist variable names that are reserved as macros. When used in Scripting, these can return, and in some cases set a value.

## Macros without input

|Macro|Return Type|Function|
|----|----|----|
|crystals|Integer or null|Returns the crystal count**\***|
|ore|Integer or null|Returns the ore count**\***|
|studs|Integer or null|Returns the studs count**\***|
|air|Integer|Returns the air status in miner-seconds**\***|
|miners|Integer|Returns the amount of miners|
|vehicles|Integer|Returns the amount of vehicles|
|buildings|Integer|Returns the amount of buildings|
|time|Integer|Returns the amount of seconds that have passed since the level began.|
|get|get(ROW)(COLUMN)|Returns the tile ID of the specified coordinates.|
|`[Class](_pages/Classes)`|Integer|Returns the amount of existing units/buildings of the specified class.**\*\***|
|lastminer||Return the last miner that activated a trigger.|
|lastvehicle||Return the last vehicle that activated a trigger.|
|lastbuilding||Return the last building that activated a trigger.|
|ConstructedBuilding||Return the last constructed building.|
|datafield|various|properties that return information about a unit or building. See [[Datafields]] for more info.|

?> \* These macros can also be used to directly set the current gathered resources (such as crystals=5).
?> \*\* You can fetch the current count of any class in the game if you know the name of it. A full list of classes is **LINK**. Buildings and vehicles **will only monitor non-hidden units**.

## Macros with input
This macro requires input values in order to function.

|Macro|Return Type|Description|
|----|----|----|
|random(MIN)(MAX)|Integer or float|Return a random number in the range [MIN-MAX]. Can be used with both integers and floats.|

## Example
	
	int CrystalGoal=3
	string myMsg=You have collected 3 crystals!
	
	if(crystals>=CrystalGoal)(msg:myMsg)
The above code make the game display a message when the player has collected 3 or more crystals.