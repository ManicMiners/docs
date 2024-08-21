# Miner Class
The miner class is used to create a reference to a miner. With that reference you can then call on and use triggers exclusive to that miner.

## Declaration
```mms
miner Charlie=2   # miner with ID of 2
miner Charlie     # miner unassigned, will be assigned later.
```

- Miner variables not assigned may later be assigned via `=lastminer` or `save`.
- Miner variables may be assigned to each other.
- Unassigned Miner variables cannot be used in a trigger.
- It is common to use `miner` collection class in the trigger and use `=lastminer` or `save` in an event chain.
- Undiscovered miners and their triggers are inactive until they are discovered.

>Specifying an id only works on miners that are part of the map. There is no way to dynamically assign at runtime a miner using the id.

## Properties
These are the class properties specific to miners.  Properties start with the dot `.` character followed by the name after the object variable or collection name.


## Trigger Properties 
>These properties are for use in triggers. They cannot be used in assignments or conditions.

|Name|Description|
|---|---|
|dead|Trigger when a miner dies.|
|new|Trigger when a miner is created. Requires collection. |
|click|Trigger when a miner is clicked.|
|hurt|Trigger when a miner take damage.|
|levelup|Trigger when miners upgrade level is increased.|

## Properties
>These properties are read-only and are used as a macro, returning a value. They may be used in assignment events on the right side, or in conditions for testing. These cannot be used on collections, they must be used with a specific miner.

|Property|Type|Note|
|---|---|---|
|col|int|Returns column of the miner.|
|column|int|Returns column of the miner. Same as col.|
|health|int|Returns current hitpoints. Same has hp.|
|hp|int|Returns current hitpoints. Same has health.|
|level|int|Returns upgrade level of the miner.|
|row|int|Returns row of the miner.|
|stamina|int|same as hp.|
|tile|int|TileID miner is over|
|tileid|int|same as tile|
|X|int|Column, 300 values per cell|
|Y|int|Row, 300 values per cell|
|Z|int|Height, 300 values per cell|

Note: that there does not appear to be any way to detect miners skills.

## Collections

>Undiscovered miners are inactive and do not receive triggers until they are discovered. There is only a single special collection for miners.


`miner` keyword may be used as a collection in triggers.  It is a special collection in that it cannot be used as a macro to return number of miners but can be used in triggers. To detect every new miner:
```msg
when(miner.new)[MyNewMinerChain]
```

The `miners` read-only macro returns the number of miners.

## enable / disable
The `enable` and `disable` events support disabling transporting of miners and re-enabling. See [Events](_pages/Events).

|Event|Description|
|---|---|
|disable:miners|Disable transporting down new miners.|
|enable:miners|Enable transporting down new miners.|

## Examples 

### A miner gets teleported 

```mms
	#First we bind our variable to a object of the miner class.
	miner Charlie=3
	
	#Then we create a message to display upon him being teleported.
	string MyString="Oh no! We lost Charlie!"

	#Then the event itself.
	when(Charlie.dead)[msg:MyString]
```

When the miner Charlie gets teleported up a message will be displayed.