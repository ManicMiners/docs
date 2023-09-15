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
|clock|Integer or Float|Returns the amount of seconds that have passed since the level began. Same as time.|
|time|Integer or Float|Returns the amount of seconds that have passed since the level began. Same as clock.|
|creatures|Integer|Returns number of creatures.|
|monsters|Integer|Returns number of monsters.|
|slugs|Integer|Returns number of slimy slugs.|
|erosionscale|Float or null|Returns or sets the erosionscale.|
|hostiles|Integer|TODO Returns number of hostile units|
|get|get(ROW)(COLUMN)|Returns the tile ID of the specified coordinates.|
|[`Class`](_pages/Classes)|Integer|Returns the amount of existing units/buildings of the specified class.**\*\***|
|lastminer||Return the last miner that activated a trigger.|
|lastvehicle||Return the last vehicle that activated a trigger.|
|lastbuilding||Return the last building that activated a trigger.|
|lastcreature||Return the last creature that activated a trigger. TODO TEST|
|ConstructedBuilding||Return the last constructed building.|
|datafield|various|properties that return information about a unit or building. See [[Datafields]] for more info.|
|lava|Integer|Returns tile id of lava (6).|
|water|Integer|Returns tile id of water (11).|
|slug_hole|Integer|Returns tile id of slimy slug hole (12).|
|progress_path|Integer|Returns tile id of a progress path (13).|
|building_path|Integer|Returns tile id of a building path (14).|
|dirt|Integer|Returns tile id of dirt (26).|
|loose_rock|Integer|Returns tile id of loose rock (30).|
|hard_rock|Integer|Returns tile id of hard rock (34).|
|solid_rock|Integer|Returns tile id of solid rock (38).|
|crystal_seam|Integer|Returns tile id of a crystal seam (42).|
|ore_seam|Integer|Returns tile id of an ore seam (46).|

?> **\*** These macros can also be used to directly set the current gathered resources (such as crystals=5).
<br>**\*\*** You can fetch the current count of any class in the game if you know the name of it. A full list of classes is **LINK**. Buildings and vehicles **will only monitor non-hidden units**.

## Macros with input
This macro requires input values in order to function.

|Macro|Return Type|Description|
|----|----|----|
|random(MIN)(MAX)|Integer or float|Return a random number in the range [MIN-MAX]. Can be used with both integers and floats.|

## Example

```mms	
	int CrystalGoal=3
	string myMsg=You have collected 3 crystals!
	
	if(crystals>=CrystalGoal)(msg:myMsg)
```

The above code make the game display a message when the player has collected 3 or more crystals.