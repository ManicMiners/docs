# Miner Class
The miner class is used to create a reference to a miner. With that reference you can then call on and use triggers exclusive to that miner.
## Declaration

```mms
	miner Charlie=2
```

This declares the miner with an ID of 2 as Charlie. The ID is given to miners based on the order they are placed in the level. The ID can be manually changed inside the level file.

## Collection 
The miner collection can be used together with triggers to execute events when something happens to any miner in the level.

### Disable or enable the teleportation of miners 
The miner collection can be used together with the disable event in order to prevent the player from teleporting down miners. Likewise the enable event will re-allow a player to teleport down miners.
disable:miners
enable:miners

## Triggers 

|Name|Description|
|---|---|
|dead|Trigger when a miner dies.|
|new|Trigger when a miner is created.|
|click|Trigger when a miner is clicked.|
|hurt|Trigger when a miner take damage.|
|upgraded|Trigger when miner is upgraded.|

## Properties

|Property|Type|Note|
|---|---|---|
|col|Integer|Returns column of the miner.|
|column|Integer|Returns column of the miner. Same as col.|
|health|Integer|Returns current hitpoints. Same has hp.|
|hp|Integer|Returns current hitpoints. Same has health.|
|level|Integer|Returns upgrade level of the miner.|
|row|Integer|Returns row of the miner.|
|stamina|Integer|Returns stamina. TODO what is that?|
|tile|Integer|TODO unknown. Same as tileid.|
|tileid|Integer|TODO unknown. Same as tile.|
|X|Integer|Column, 300 values per cell|
|Y|Integer|Row, 300 values per cell|
|Z|Integer|Height - TODO UNITS?|

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