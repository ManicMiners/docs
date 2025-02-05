# Building Class
The building class is used to create a reference to a building. With that reference you can then call on and use triggers and properties exclusive to that building. You may also refer to a building collection where you may use triggers connected to every building of a specific type.

## Declaration

```mms
building MyBuilding=2,14  # existing building at row 2, col 14 assigned to variable
building MyBuilding       # will be assigned later.
```

- Building variables not assigned may later be assigned via `=lastbuilding` or `savebuilding`.
- Building variables may be assigned to each other.
- Unassigned building variables cannot be used in a trigger.
- It is common to use a building collection class in the trigger and use `=lastbuilding` or `savebuilding` in an event chain to get the building that caused the trigger.
- Undiscovered buildings and their triggers are inactive until they are discovered.

>Specifying a row,col only works on buildings that are part of the map. There is no way to dynamically assign at runtime a building using the row,col format.

## Properties
These are the class properties specific to buildings.  Properties start with the dot `.` character followed by the name after the object variable or collection name.

## Trigger properties
>These properties are for use in triggers. They cannot be used in assignments or conditions.

|Name|Description|
|---|---|
|built:row,col|Trigger when a building is built covering the row,col. Requires collection.|
|click|Trigger when a building is clicked.|
|dead|Trigger when a building gets teleported up.|
|hurt|Trigger when a building take damage.|
|levelup|Trigger when building is leveled up.|
|new|Trigger when a building is created. Requires collection.|
|poweroff|Trigger when power is deactivated for a building.|
|poweron|Trigger when power is activated for a building.|

## Properties
>These properties are read-only and are used as a macro, returning a value. They may be used in assignment events on the right side, or in conditions for testing. These cannot be used on collections, they must be used with a specific building.

|Property|Type|Note|
|---|---|---|
|col|int|Returns column of the building. Same as column.|
|column|int|Returns column of the building. Same as col.|
|health|int|Returns current hitpoints. Same has hp.|
|hp|int|Returns current hitpoints. Same has health.|
|ispowered|bool|Same as power.|
|level|int|Returns upgrade level of the building.|
|power|bool|Returns `true` if the building has power, `false` if it doesn't.|
|powered|bool|Same as power.|
|row|int|Returns row of the building.|
|tile|int|TileID for the initial place point of the building.|
|tileid|int|Same as tile.|
|X|int|Column, 300 values per map tile.|
|Y|int|Row, 300 values per map tile.|
|Z|int|Height, 300 values per map tile.|

>Note that there is no id property on buildings.

## Collections 
Each native building class has their own collection. When used by itself without a trigger property, it is treated as a read-only macro returning the total number of constructed buildings of that type. Collections may only use trigger properties.

>Undiscovered buildings are inactive and do not receive triggers until they are discovered.

|Name|Note|
|---|---|
|building|Refers to all buildings.|
|BuildingCanteen_C|Canteen.|
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

> `building` is a special collection in that it cannot be used as a macro to return number of buildings but can be used in triggers. To detect every new building:
```mms
when(building.new)[MyNewBuildingChain]  # call event chain when any building is created.
```

## Macros
These are not collections - they are macros. They return the number of objects as an int. They may be used in assignments on the right side or in conditions.

|Name|Description|
|---|---|
|buildings|Number of all buildings.|
|canteen|Number of Canteens.|
|docks|Number of Docks.|
|electricfence|Number of Fences.|
|ElectricFence_C|Number of fence objects. Not a collection.|
|geologicalcenter|Number of Geological Centers.|
|mininglaser|Number of Mining Lasers.|
|orerefinery|Number of Ore Refineries.|
|powerstation|Number of Power Stations.|
|superteleport|Number of Super Teleports.|
|supportstation|Number of Support Stations.|
|teleportpad|Number of Teleport Pads.|
|toolstore|Number of Tool Stores.|
|upgradestation|Number of Upgrade Stations.|

## Disable or enable a building
A collection can be used together with the disable event in order to prevent the player from creating a specified building. Likewise the enable event will re-allow a player to construct the specified building. See [Events](_pages/Events).

```mms
disable:BuildingSuperTeleport_C
enable:BuildingSuperTeleport_C
disable:buildings   # buildings is a special keyword referring to all buildings in this context.
enable:buildings    # buildings is a special keyword referring to all buildings in this context
```

## Electric Fence
There is very little script can do to track and work with electric fences.  There are are two macros that return the number of placed electric fences:  `ElectricFence_C` and `electricfence`. `BuildingElectricFence_C` collection can be also used as a macro to return the same value.

While `BuildingElectricFence_C` is a collection - it is subject to limitations:
- new and built property triggers do not fire - they do not appear to be hooked up internally.
- since there is no way for a fence to cause a trigger, it is not possible to get a fence via `lastbuilding` event.
- read only property `powered` does work but it needs a variable for a single fence so it is not possible to detect the state of any user placed fences.

Even if triggers would work, generally players place a number of fences and since there is no array for buildings, there is no way to keep track of fences. Also fences can be placed in any order and at some point after the fence is placed it may gain or lose power and there are no triggers for power state changes.

Thus the only operation script really has is the ability to read the number of placed fences.

## Examples
### Display number of support stations after every one is created.

```mms
when(BuildingSupportStation_C.new)[msg:BuildingSupportStation_C]
```


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