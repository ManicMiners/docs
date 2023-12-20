# Building Class
The building class is used to create a reference to a building. With that reference you can then call on and use triggers and properties exclusive to that building. You may also refer to a building collection where you may use triggers connected to every building of a specific type.

## Declaration

```mms
building MyStore=2,14  # existing building at row 2, col 14 assigned to variable
building MyStore       # will be assigned later.
```

- Building variables not assigned may later be assigned via `=lastbuilding` or `savebuilding`.
- Building variables may be assigned to each other.
- Unassigned building variables cannot be used in a trigger.
- It is common to use a building collection class in the trigger and use `=lastbuilding` or `savebuilding` in an event chain.
- Undiscovered buildings and their triggers are inactive until they are discovered.

## Triggers

|Name|Description|
|---|---|
|built|Trigger when a building is built. Requires collection.|
|click|Trigger when a building is clicked.|
|dead|Trigger when a building gets teleported up.|
|hurt|Trigger when a building take damage.|
|levelup|Trigger when building is leveled up.|
|new|Trigger when a building is created. Requires collection.|
|poweroff|Trigger when power is deactivated for a building.|
|poweron|Trigger when power is activated for a building.|

## Properties

|Property|Type|Note|
|---|---|---|
|col|int|Returns column of the building. Same as column.|
|column|int|Returns column of the building. Same as col.|
|health|int|Returns current hitpoints. Same has hp.|
|hp|int|Returns current hitpoints. Same has health.|
|id|int|Returns the ID the building.|
|ispowered|bool|Same as power.|
|level|int|Returns upgrade level of the building.|
|power|bool|Returns TRUE if the building has power, FALSE if it doesn't.|
|powered|bool|Same as power.|
|row|int|Returns row of the building.|
|stamina|int|same as hp.|
|tile|int|TileID for the initial place point of the building.|
|tileid|int|same as tile.|
|X|int|Column, 300 values per cell|
|Y|int|Row, 300 values per cell|
|Z|int|Height, 300 values per cell|


## Collections 
Each native building class has their own collection. When used by itself the collection return the total number of constructed buildings of that type. The collection can utilize triggers but not properties. Buildings must be discovered, undiscovered buildings are inactive until they are discovered.

|Name|Note|
|---|---|
|BuildingDocks_C|Docks.|
|BuildingElectricFence_C|Electric Fences.|
|BuildingGeologicalCenter_C|Geological Centers.|
|BuildingMiningLaser_C|Mining Lasers.|
|BuildingOreRefinery_C|Ore Refineries.|
|BuildingPowerPath_C|Power Paths. This object is deleted when construction is finished.|
|BuildingPowerStation_C|Power Stations.|
|BuildingSuperTeleport_C|Super Teleports.|
|BuildingSupportStation_C|Support Stations.|
|BuildingTeleportPad_C|Teleport Pads.|
|BuildingToolStore_C|Tool Stores.|
|BuildingUpgradeStation_C|Upgrade Stations.|

> `building` keyword may also be used as a collection in triggers.  It is a special collection in that it cannot be used as a macro to return number of buildings but can be used in triggers. To detect every new building:
```mms
when(building.new)[MyNewBuildingChain]
```

## Macros
These are not collections. They return the number of objects as an int.

|Name|Description|
|---|---|
|buildings|Number of all buildings.|
|docks|Number of Docks.|
|electricfence|Number of Fences.|
|ElectricFence_C|Number of fence objects. Not a collection.|
|geologicalcenter|Number of Geological Centers.|
|mininglaser|Number of Geological Centers.|
|orerefinery|Number of Ore Refineries.|
|powerstation|Number of Power Stations.|
|supportstation|Number of Support Stations.|
|teleportpad|Numbewr of Teleport Pads.|
|toolstore|Number of Tool Stores.|
|upgradestation|Number of Upgrade Stations.|

## Disable or enable a building
A collection can be used together with the disable event in order to prevent the player from creating a specified building. Likewise the enable event will re-allow a player to construct the specified building. See [Events](_pages/Events).

```mms
disable:BuildingSuperTeleport_C
enable:BuildingSuperTeleport_C
disable:buildings   # notice buildings is special keyword - not a macro.
```

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