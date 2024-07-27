# DAT Section miners

The miners section lists all of the starting miners in the game. Each miner is on its own line, and every miner has a unique ID number.

Miners are from level one through level five, may carry up to five items, and be trained in up to six jobs. They may be flagged as essential, and the player will lose the map if the miner is teleported for any reason.

Miners listed in the objectives sections must also be in the miners section. Miners listed in the vehicle section as driving a vehicle must exist in the miners section.

Format:

```
ID,TRANSLATION,OPTIONS,ESSENTIAL
```

## ID

Required field. Every starting miner has a unique miner ID automatically filled in by the map editor. Once that miner has left the game, any script variable associated with that miner is now invalid, any triggers for that variable are invalid, and the ID is then reused for new miners transported down.

```
ID=value
```
value is the id of the miners. ID's start at 0 and increment by one for every miner in the game. 

## TRANSLATION

Required field, it provides the translation (offset), rotations, and scale for the miner. The editor will automatically compute these values for you so that the miner is correctly placed on the floor tiles. By changing these values you may manually bury part or all of a miner or cause it to float in the air. Miners that are not correctly placed on the floor may be unusable.

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

## OPTIONS

This is a list of optional options, each ending in a forward slash character with no spaces. Options may be jobs known by the miner, objects carried by the miner or its level.  While the order during map load, the editor always writes the options in the order of: objects/jobs/level


### Objects
Objects are all optional.

- Drill/ 
- Shovel/ 
- Hammer/ 
- Spanner/ 
- Sandwich/ 

Weapons:

- BeamLaser/ 
- BeamFreezer/ 
- BeamPusher/ 
- SonicBlasterTool/ 
 
> Only one of the four weapons may be carried. It is not valid to list multiple weapons for the same miner.

> The level of the miner determines how many objects they may hold. Every miner starts at level one and may hold two items, each increase in level lets the miner hold an additional item. Thus a level 5 miner may hold all 5 objects plus one of the weapons.

### Jobs
Jobs are all optional. Miners may learn up to six jobs (skills).

- JobExplosivesExpert/ 
- JobDriver/ 
- JobEngineer/ 
- JobGeologist/ 
- JobPilot/ 
- JobSailor/ 

### Level
By default every miner is level 1. Each use of the `Level/` tag increases the miner level, thus a level five miner will have 4 upgrades.
```
Level/Level/Level/Level/
```

## ESSENTIAL

Optional value - miners that are essential for the player to complete the map have this tag. This means if the miner is teleported in any manner including manual teleportation, will cause the player to lose the map. These miners will have a floating star over them to identify them as essential.

Format:
```
Essential=true
```

## Example
Within a 8x8 map, a level 5 miner carrying all tools and a pusher beam and knows all jobs and is essential.

```
ID=4,Translation: X=1644.653 Y=1701.715 Z=53.095 Rotation: P=0.000000 Y=142.691574 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000,Drill/BeamPusher/Sandwich/Spanner/Hammer/Shovel/JobExplosivesExpert/JobDriver/JobEngineer/JobGeologist/JobPilot/JobSailor/Level/Level/Level/Level/,Essential=true
```
