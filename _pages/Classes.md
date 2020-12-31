# Classes

Not all classes of the game are known. See the bottom of this page on how you can learn more about them. Also don't forget to share anything you discover so that the wiki can be updated.

## General information 
A class can imply a declaration of an object type or a reference to a collection of objects. Currently classes can be divided in the following subcategories:

- Buildings
- Vehicles
- Items
- Environmental

### Declaration 
A variable is declared a object of a certain type, for example a miner.

	miner myMiner=1

### Collection 
A group of objects of a specific type or category, for example miners or Support Stations

	miners
	BuildingSupportStation_C

### Usage
Declared objects or collections can be used together with triggers or properties, for example:

	when(myMiner.dead)[EVENT]

Trigger when the specified miner gets teleported back up.

	when(BuildingSupportStation_C.new)[EVENT]

Trigger when a Support Station is built.

	when(MyBuilding.click)((MyBuilding.power==true))[EVENT]

Trigger when a building is clicked but only if the building is currently powered and not turned off.
<hr>
Complete examples can be found in the pages for the larger classes and in the scripting examples page.

## Class-types 
A class can either be **curated** or **non-curated**, this refer to wheter the class have a predictable behaviour or not. Over time more classes will become curated as the game is developed further.

### Curated
Curated classes are officially supported, therefore they have predictable behaviour. For example, asking the game for the amount of Support Stations will return all constructed Support Stations, buildings under construction will not be counted. The following scripts are supported:

- Count macros
- Monitor events
- Enable/Disable events

### Non-curated 
These classes can be used in some instances. These classes can have undefined return values for certain classes. For example, if you try to check how many Crystals are in the level, you will get both rechargable and charged crystals with no way of sorting them.

## Class triggers 
Class triggers are predefined triggers bound to specific object types. For triggers connected to larger classes, see their respective wiki-page. 

	CLASS.Trigger

Where CLASS is replaced with a collection or declared object and trigger with a valid trigger:

|Command|Meaning|
|----|----|
|miner|Trigger if the event occur to any miner except miners named with variables.|
|vehicle|Trigger if the event occur to any vehicle except vehicles named with variables.|
|collection|Trigger when the specified event occur to any object of that collection.|
|named object|Trigger if the event occur to that specific object.|

?> Triggering a named object can also execute a trigger for a collection that includes that object.

**List of common triggers**

|Name|Description|
|---|---|
|dead|Trigger when a object dies or get teleported.|
|new|Trigger when a object is created.|
|click|Trigger when a object is clicked.|
|hurt|Trigger when a object take damage.|

## Known classes 
### Larger classes 
- [Buildings](_pages/ClassesBuildings)
- [Vehicles](_pages/ClassesVehicles)
- [Miners](_pages/ClassesMiners)

### Smaller classes 

**Items**

|Name|Curated|Note|
|---|---|---|
|Crystal_C|No||
|Ore_C|No||
|Stud_C|No||
|Barrier_C|No||
|Dynamite_C|No||
|ElectricFence_C|No|The fence item and fence building are two separate objects.|

**Environmental**

|Name|Curated|Note|
|---|---|---|
|EventErosion_C|No|Ongoing erosions. Only exists if they are active!|
|EventLandslide_C|No|Ongoing landslides. Only exists if they are active!|
|RechargeSeamGoal_C|No|Visible recharge seams. Can be used to count them.|
|NavModifierLava_C |No|Amount of lava tiles.|
|NavModifierWater_C|No|Amount of water tiles.|
|NavModifierPowerPath_C|No|Amount of Power Path tiles, any type. Only finished paths.|
|NavModifierRubble_C|No|Amount of Rubble tiles, any stage.|

## More classes
If you have an interest in a specific type of class to be added to this page, you can personally request them from the developer or check an older unpacked game build. In the unpacked build, every class has its own object. Please note that some class names have changed between different builds of the game.