# DAT Section vehicles

The vehicles section lists all of the vehicles in the map. These vehicles do not have to be visible, they may be in undiscovered caverns.

Each vehicle is on its own line. There is no known limit to the number of vehicles in a map. 

Vehicles may be marked as essential, if the player in any way loses the vehicle - they lose the map.

Optionally a miner may be the driver, in that case the miner is also listed in the miner section.

Format:
```
COLLECTION,TRANSLATION,UPGRADES,DRIVER,ID,ESSENTIAL
```

## COLLECTION

Required field, it names the vehicle collection class. It may be one of the following:

- VehicleCargoCarrier_C
- VehicleChromeCrusher_C
- VehicleGraniteGrinder_C
- VehicleHoverScout_C
- VehicleLMLC_C
- VehicleLoaderDozer_C
- VehicleRapidRider_C
- VehicleSmallDigger_C
- VehicleSmallTransportTruck_C
- VehicleSMLC_C
- VehicleTunnelScout_C
- VehicleTunnelTransport_C


## TRANSLATION

Required field, it provides the translation (offset), rotations, and scale for the vehicle. The editor will automatically compute these values for you so that the vehicle is correctly placed on the floor tiles. By changing these values you may manually bury part or all of a vehicle or cause it to float in the air. Vehicles that are not correctly placed on the floor may be unusable.

Format:
```
Translation: X=value Y=value Z=value Rotation: P=value Y=value R=value Scale X=value Y=value Z=value
```

Translation:
- X= floating point X location, this is in 300 units per tile. This is the same value returned by the .X data member.
- Y= floating point Y location, this is in 300 units per tile. This is the same value returned by the .Y data member.
- Z= floating point Z location, this is in 300 units per tile. This is the same value returned by the .Z data member.

Rotation:
- P= floating point in degrees (-180 - 180). Pitch around the X axis.
- Y= floating point in degrees (-180 - 180). Yaw around the Y axis.
- R= floating point in degrees (-180 - 180), Roll around the Z axis.

Scale  (notice no colon character)
- X= floating point X scale, default is 1.0.
- Y= floating point Y scale, default is 1.0.
- Z= floating point Z scale, default is 1.0.

## UPGRADES

Optional value - only valid for vehicles that may be updated. Vehicles have class specific upgrades.

```
upgrades=name1/name2/...
```

Where the names are valid upgrades for each vehicle class. Each upgrade ends in a forward slash. There are no spaces anywhere.

Upgrades for each vehicle class:

|Vehicle class|Upgrades|
|---|---|
|VehicleCargoCarrier_C|UpAddNav/ |
|VehicleChromeCrusher_C|UpDrill/ UpLaser/ UpScanner/ UpEngine/ |
|VehicleGraniteGrinder_C|UpDrill/ UpEngine/ |
|VehicleHoverScout_C|UpEngine/ |
|VehicleLMLC_C|UpEngine/ UpLaser/ UpAddNav |
|VehicleLoaderDozer_C|UpEngine/ |
|VehicleRapidRider_C|UpCargoHold/ UpAddDrill/ |
|VehicleSmallDigger_C|UpDrill/ UpEngine/ |
|VehicleSmallTransportTruck_C|UpCargoHold/ UpEngine/|
|VehicleSMLC_C|UpEngine/ UpLaser/ |
|VehicleTunnelScout_C|UpAddDrill/ |
|VehicleTunnelTransport_C|NONE |

>VehicleTunnelTransport_C has no upgrades and cannot have the Upgrades= field.

>LMLC has a hidden upgrade `UpAddNav` which allows the vehicle to travel over lava. It can only be applied to vehicles defined in the map file. Currently there is no way for a user to add this upgrade in game.
## DRIVER

Optional value - has the miner id that is driving the vehicle. If a miner is not driving, this field is missing.
```
driver=value
```
value is the Miner ID from the section miners.

## ID
Required field. Every starting vehicle has a unique vehicle ID automatically filled in by the map editor. Once that vehicle has left the game, any script variable associated with that vehicle is now invalid, any triggers for that variable are invalid, and the ID is then reused for new vehicles transported down.

```
ID=value
```
value is the id of the vehicle. ID's start at 0 and increment by one for every vehicle in the game. 

## ESSENTIAL

Optional value - vehicles that are essential for the player to complete the map have this tag. This means if the vehicle is destroyed or lost in any manner including manual teleportation, will cause the player to lose the map. These vehicles will have a floating star over them to identify them as essential.

Format:
```
Essential=true
```

# Example

Within an 8x8 map,  Chrome Crusher that has all upgrades, a driver, and is essential. The ID for this vehicle is 9, and the miner ID is 2 (so a miner with an ID of 2 will be in the sections miners).

```
VehicleChromeCrusher_C,Translation: X=1138.967 Y=673.896 Z=0.187 Rotation: P=-0.000061 Y=-77.706703 R=-0.237549 Scale X=1.000 Y=1.000 Z=1.000,upgrades=UpDrill/UpLaser/UpScanner/UpEngine/,driver=2,ID=9,Essential=true
```
