# DAT Section buildings

The buildings section lists all of the buildings in the map. These buildings do not have to be visible, they may be in undiscovered caverns.

Buildings may be part of an objective, in that case they are listed in both the objectives and buildings section.

Each building is on its own line. There is no known limit to the number of buildings in a map. Undefined behavior may occur if buildings overlap each other. Buildings are not subject to map editor placement rules - the engine will try as best as possible to put the building in the given location with the provided rotation and scale. A building may be unusable if incorrectly placed.

Buildings may be marked as essential, if the player in any way loses the building - they lose the map.

> Buildings do not have an ID!

Format:
```
COLLECTION,TRANSLATION,LEVEL,TELEPORT,ESSENTIAL
```

## COLLECTION

Required field, it names the building collection class. It may be one of the following:

- BuildingCanteen_C
- BuildingDocks_C
- BuildingElectricFence_C
- BuildingGeologicalCenter_C
- BuildingMiningLaser_C
- BuildingOreRefinery_C
- BuildingPowerStation_C
- BuildingSuperTeleport_C
- BuildingSupportStation_C
- BuildingUpgradeStation_C
- BuildingTeleportPad_C
- BuildingToolStore_C


## TRANSLATION

Required field, it provides the translation (offset), rotations, and scale for the building. The editor will automatically compute these values for you so that the building is correctly placed on the floor tiles. By changing these values you may manually bury part or all of a building or cause it to float in the air. Buildings that are not correctly placed on the floor may be unusable.

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

## LEVEL

Optional value - only valid for building that may be updated. Provides the upgrade level

```
Level=value
```

Where the value is the upgrade level of the building. The value must be a valid upgrade level for that building. By default, all buildings have a level 1.

## TELEPORT

Optional value - buildings that are intended to display teleport down animation at map start or after discovery will have this value.

Format:
```
Teleport=True
```

By default every building has a false value - it will be fully shown instantly upon discovery or map load.

## ESSENTIAL

Optional value - buildings that are essential for the player to complete the map have this tag. This means if the building is destroyed or lost in any manner including manual teleportation, will cause the player to lose the map. These buildings will have a floating star over them to identify them as essential.

Format:
```
Essential=true
```

# Examples

Within an 8x8 map, a level 3 toolstore that will teleport in at the beginning of the mission and be essential.

```
BuildingToolStore_C,Translation: X=1650.000 Y=1350.000 Z=0.000 Rotation: P=0.000000 Y=-179.999954 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000,Level=3,Teleport=True,Essential=true
```

A level 1 toolstore that is shown instantly at map load that is not essential.

```
BuildingToolStore_C,Translation: X=1650.000 Y=1350.000 Z=0.000 Rotation: P=0.000000 Y=-179.999954 R=0.000000 Scale X=1.000 Y=1.000 Z=1.0
```
