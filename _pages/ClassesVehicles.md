# Vehicle Class
The vehicle class is used to create a reference to a vehicle. With that reference you can then call on and use triggers and properties exclusive to that vehicle. You may also refer to a vehicle collection where you may use triggers connected to every vehicle of a specific type.
## Declaration

```mms
vehicle Sofia=2    # existing vehicle id of 2 is assigned to variable Sofia
vehicle Sofia      # unassigned vehicle, will be assigned later
```

- Vehicle variables not assigned may later be assigned via `=lastvehicle` or `savevehicle`.
- Vehicle variables may be assigned to each other.
- Unassigned vehicle variables cannot be used in a trigger.
- It is common to use a vehicle collection class in the trigger and use `=lastvehicle` or `savevehicle` in an event chain.
- Undiscovered vehicles and their triggers are inactive until they are discovered.

## Triggers 
Triggers may be used on a single object variable or on collections.

|Name|Description|
|---|---|
|click|Trigger when a vehicle is clicked.|
|dead|Trigger when a vehicle dies.|
|driven|Trigger when a miner enters a vehicle.|
|hurt|Trigger when a vehicle takes damage.|
|new|Trigger when a vehicle is created. Collection required.|
|upgrade|Trigger when vehicle is upgraded.|

## Properties
Properties may only be used on a single object, they are not for use with collections.

|Property|Type|Note|
|---|---|---|
|col|int|Returns column of the vehicle.|
|column|int|Returns column of the vehicle. Same as col.|
|driver|int|miner id of the driver. Same as driverid.|
|driverid|int|miner id of the driver. Same as driver.|
|health|int|Returns current hitpoints. Same has hp.|
|hp|int|Returns current hitpoints. Same has health.|
|id|int|Returns the ID the vehicle.|
|row|int|Returns row of the vehicle.|
|tile|int|Current tile ID vehicle is over. Same as tileid.|
|tileid|int|Current tile ID vehicle is over. Same as tile.|
|X|int|Column, 300 values per cell|
|Y|int|Row, 300 values per cell|
|Z|int|Height - units are from height value in map

Note: there is no level property on vehicles to query upgrades

## Collections
Each native vehicle class has their own collection. When used by itself the collection return the total amount of constructed vehicles of that type. The collection can utilize triggers but not properties.

> `vehicle` keyword may also be used as a collection in triggers.  It is a special collection in that it cannot be used as a macro to return number of vehicles but can be used in triggers. To detect every new vehicle:
```msg
when(vehicle.new)[MyNewVehicleChain]
```


### Disable or enable a vehicle
A collection can be used together with the disable event in order to prevent the player from teleporting down the specified vehicle. Likewise the enable event will re-allow a player to teleport the specified vehicle. See [Events](_pages/Events).

```mms
disable:VehicleChromeCrusher_C
enable:VehicleChromeCrusher_C
disable:vehicles
```

### List of collections 
Collections may be used by as a macro to return an int the is the number of those objects in the map. Undiscovered objects are not included in the count.
Collections may be used as a trigger.

|Name|Description|
|---|---|
|VehicleCargoCarrier_C|Cargo Carriers|
|VehicleChromeCrusher_C|Chrome Crushers|
|VehicleGraniteGrinder_C|Granite Grinders|
|VehicleHoverScout_C|Hover Scouts|
|VehicleLMLC_C|Large Mobile Laser Cutters|
|VehicleLoaderDozer_C|Loader Dozers|
|VehicleRapidRider_C|Rapid Riders|
|VehicleSmallDigger_C|Small Diggers|
|VehicleSmallTransportTruck_C|Small Transport Trucks|
|VehicleSMLC_C|Small Mobile Laser Cutter|
|VehicleTunnelScout_C|Tunnel Scouts|
|VehicleTunnelTransport_C|Tunnel Transports|

## Macros
These are not collections. They return the number of objects as an int.

|Name|Description|
|---|---|
|cargocarrier|Number of Cargo Carriers.|
|chromecrusher|Number of Chrome Crushers.|
|granitegrinder|Number of Granite Grinders.|
|hoverscout|Number of Hover Scouts.|
|LMLC|Number of Large Mobile Laser Cutters.|
|loaderdozer|Number of Loader Dozers.|
|rapidrider|Number of Rapid Riders.|
|smalldigger|Number of Small Diggers.|
|smalltransporttruck|Number of Small Transport Trucks.|
|SMLC|Number of Small Mobile Laser Cutters|
|tunnelscout|Number of Tunnel Scouts.|
|tunneltransport|Number of Tunnel Transports.|
|vehicles|Number of vehicles.|


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