# Building Class
The building class is used to create a reference to a building. With that reference you can then call on and use triggers and properties exclusive to that building. You may also refer to a building collection where you may use triggers connected to every building of a specific type.

## Declaration

```mms
	building MyStore=2,14
```

This declares the building at row 2, column 14 as `MyStore`.

## Triggers

|Name|Description|
|---|---|
|dead|Trigger when a building gets teleported up.|
|new|Trigger when a building is created.|
|click|Trigger when a building is clicked.|
|hurt|Trigger when a building take damage.|
|built|Trigger when a building is built.|
|poweron|Trigger when power is activated for a building.|
|poweroff|Trigger when power is deactivated for a building.|
|upgraded|Trigger when building is upgraded.|

## Properties

|Property|Type|Note|
|---|---|---|
|col|Integer|Returns column of the building. Same as column.|
|column|Integer|Returns column of the building. Same as col.|
|health|Integer|Returns current hitpoints. Same has hp.|
|hp|Integer|Returns current hitpoints. Same has health.|
|id|Integer|Returns the ID the building.|
|ispowered|Boolean|Same as power.|
|level|Integer|Returns upgrade level of the building.|
|power|Boolean|Returns TRUE if the building has power, FALSE if it doesn't.|
|powered|Boolean|Same as power.|
|row|Integer|Returns row of the building.|
|stamina|Integer|same as hp.|
|tile|Integer|TileID for the initial place point of the building.|
|tileid|Integer|same as tile.|
|X|Integer|Column, 300 values per cell|
|Y|Integer|Row, 300 values per cell|
|Z|Integer|Height, 300 values per cell|


## Collections 
Each native building class have their own collection. When used by itself the collection return the total amount of constructed buildings of that type. The collection can utlize triggers but not properties.

### Disable or enable a building
A collection can be used together with the disable event in order to prevent the player from creating a specified building. Likewise the enable event will re-allow a player to construct the specified building.

```mms
	disable:BuildingSuperTeleport_C
	enable:BuildingSuperTeleport_C
```

### List of collections

|Name|Curated|Note|
|---|---|---|
|BuildingToolStore_C|Yes||
|BuildingTeleportPad_C|Yes||
|BuildingDocks_C|Yes||
|BuildingPowerStation_C|Yes||
|BuildingSupportStation_C|Yes||
|BuildingUpgradeStation_C|Yes||
|BuildingGeologicalCenter_C|Yes||
|BuildingOreRefinery_C|Yes||
|BuildingMiningLaser_C|Yes||
|BuildingSuperTeleport_C|Yes||
|BuildingElectricFence_C|Yes|The fence item and fence building are two separate objects|
|BuildingPowerPath_C|Yes|This object is deleted when construction is finished|

## Examples
### Count buildings

```mms
	when(drill:2,2)[msg:BuildingSupportStation_C]
```

When you drill a wall at position 2,2 a number indicating the total amount of constructed Support 	Stations will be displayed.

### Click a building

```mms
	building MyStore=2,14
	string MyMsg="You clicked on MyStore!"
	when(MyStore.click)[msg=MyMsg]
```

When you click on the building at the given coordinates a message will be displayed.

### Click any building

```mms
	string MyMsg="You clicked on a building!"
	when(building.click)[msg=MyMsg]
```

When you click any building a message will be displayed.