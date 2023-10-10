# Vehicle Class
The vehicle class is used to create a reference to a vehicle. With that reference you can then call on and use triggers and properties exclusive to that vehicle. You may also refer to a vehicle collection where you may use triggers connected to every vehicle of a specific type.
## Declaration

```mms
	vehicle Sofia=2
```

This declares the vehicle with an ID of 2 as Sofia. The ID is given to vehicles based on the order they are placed in the level. The ID can be manually changed inside the level file.

## Triggers 

|Name|Description|
|---|---|
|dead|Trigger when a vehicle dies.|
|new|Trigger when a vehicle is created.|
|click|Trigger when a vehicle is clicked.|
|hurt|Trigger when a vehicle take damage.|
|driven|Trigger when a miner enters a vehicle.|
|upgraded|Trigger when vehicle is upgraded.|

## Properties

|Property|Type|Note|
|---|---|---|
|col|Integer|Returns column of the vehicle.|
|column|Integer|Returns column of the vehicle. Same as col.|
|driver|Integer|miner id of the driver. Same as driverid.|
|driverid|Integer|miner id of the driver. Same as driver.|
|health|Integer|Returns current hitpoints. Same has hp.|
|hp|Integer|Returns current hitpoints. Same has health.|
|id|Integer|Returns the ID the vehicle.|
|row|Integer|Returns row of the vehicle.|
|tile|Integer|Current tile ID vehicle is over. Same as tileid.|
|tileid|Integer|Current tile ID vehicle is over. Same as tile.|
|X|Integer|Column, 300 values per cell|
|Y|Integer|Row, 300 values per cell|
|Z|Integer|Height - units are from height value in map

Note: there is no level property on vehicles to query upgrade level

## Collections
Each native vehicle class have their own collection. When used by itself the collection return the total amount of constructed vehicles of that type. The collection can utilize triggers but not properties.

### Disable or enable a building 
A collection can be used together with the disable event in order to prevent the player from teleporting down the specified vehicle. Likewise the enable event will re-allow a player to teleport the specified vehicle.

```mms
	disable:VehicleChromeCrusher_C
	enable:VehicleChromeCrusher_C
```

### List of collections 

|Name|Note|
|---|---|---|
|VehicleHoverScout_C||
|VehicleSmallDigger_C||
|VehicleSmallTransportTruck_C||
|VehicleSMLC_C|Small Mobile Laser Cutter|
|VehicleRapidRider_C||
|VehicleTunnelScout_C||
|VehicleLoaderDozer_C||
|VehicleGraniteGrinder_C||
|VehicleChromeCrusher_C||
|VehicleLMLC_C|Large Mobile Laser Cutter|
|VehicleCargoCarrier_C||
|VehicleTunnelTransport_C||

## Examples 
### Vehicle gets teleported 

```mms
	vehicle Sofia=1
	
	string SofiaDied="Oh no! We lost Sofia!"
	string VehicleDied="We have lost a vehicle."
	string SmallDiggerDied="We lost a Small Digger!"
	
	when(Sofia.dead)[msg:SofiaDied]
	when(vehicle.dead)[msg:VehicleDied]
	when(VehicleSmallDigger_C.dead)[msg:SmallDiggerDied]
```

When you lose your Small Digger named Sofia you will get two messages: One because the named vehicle got teleported and one because a vehicle of the Small Digger collection got teleported. You would expect a third message being created by "vehicle.dead" but it is overriden by "Sofia.dead" which means a third message will not be displayed.

### A miner enter a vehicle 

```mms
	vehicle Sofia=1
	when(Sofia.driven)[GiantEruption]
```

When a miner enter the vehicle Sofia a chain event will be called. 