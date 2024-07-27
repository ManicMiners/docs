# DAT Section creatures

The creatures section has a slightly different format. Two of the fields are on their own lines.

Format:

```
COLLECTION
TRANSLATION
ID,HP,SLEEP
```

>Bats have no mechanic in the game - they are for visual effect only and they move around in a small swarm in a random manner. Historically Bats would scare miners but the mechanic was removed from Manic Miners since it could adversely affect game play. Bats have an ID and a creature script variable may be assigned to them and they exist for the duration of the game. Bats cannot have the HP or SLEEP properties.

## COLLECTION
This is the collection class of the creature and is one of:

- CreatureBat_C
- CreatureIceMonster_C
- CreatureLavaMonster_C
- CreatureRockMonster_C
- CreatureSlimySlug_C
- CreatureSmallSpider_C

## TRANSLATION

Required field, it provides the translation (offset), rotations, and scale for the creature. The editor will automatically compute these values for you so that the creature is correctly placed on the floor tiles. By changing these values you may manually bury part or all of a creature or cause it to float in the air. Creatures that are not correctly placed on the floor may be unusable.

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

## ID

Required field. Every starting creature has a unique creature ID automatically filled in by the map editor. Once that creature has left the game, any script variable associated with that creature is now invalid, any triggers for that variable are invalid, and the ID is then reused for new creatures spawned.

```
ID=value
```
value is the id of the creature. ID's start at 0 and increment by one for every creature in the game. 


## HP
Optional field. Bats cannot use this field. The value is the number of hit points assigned to the creature. Every creature has a maximum number of hit points that is scaled by the Scale X,Y,Z values (either higher or lower). A creature cannot have more hit points than its max.

|Class|Default HP|
|---|---|
|CreatureBat_C|NONE|
|CreatureIceMonster_C|100|
|CreatureLavaMonster_C|100|
|CreatureRockMonster_C|100|
|CreatureSlimySlug_C|100|
|CreatureSmallSpider_C|5|

## Sleep
Creatures by default are awake. If this field is used, the creature starts off sleeping. They remain asleep until a miner comes within range or the creature is attacked and then they wake up. Spiders and Bats cannot be asleep and thus cannot use this field.

```
Sleep=true
```
Indicates the creature is sleeping. If the creature is awake, this field is not used.

## Examples
Various creatures on a 8x8 map with different scales and properties.

```
CreatureSlimySlug_C
Translation: X=412.704 Y=1441.176 Z=62.150 Rotation: P=0.000000 Y=7.062748 R=0.000000 Scale X=2.000 Y=2.000 Z=2.000
ID=6,HP=200
CreatureSlimySlug_C
Translation: X=666.563 Y=1299.565 Z=62.150 Rotation: P=0.000000 Y=-102.390236 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=7,Sleep=true
CreatureLavaMonster_C
Translation: X=387.120 Y=536.119 Z=137.150 Rotation: P=0.000000 Y=-47.522785 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=8
CreatureLavaMonster_C
Translation: X=718.229 Y=407.623 Z=137.150 Rotation: P=0.000000 Y=144.381180 R=0.000000 Scale X=1.250 Y=1.250 Z=1.250
ID=9,HP=80,Sleep=true
CreatureIceMonster_C
Translation: X=1966.119 Y=466.544 Z=137.150 Rotation: P=0.000000 Y=112.179260 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=10
CreatureIceMonster_C
Translation: X=1921.523 Y=720.352 Z=137.150 Rotation: P=0.000000 Y=-133.438202 R=0.000000 Scale X=1.500 Y=1.500 Z=1.500
ID=11,HP=85,Sleep=true
CreatureRockMonster_C
Translation: X=1270.197 Y=454.853 Z=137.150 Rotation: P=0.000000 Y=-55.184422 R=0.000000 Scale X=1.500 Y=1.500 Z=1.500
ID=12,HP=70,Sleep=true
CreatureRockMonster_C
Translation: X=1339.537 Y=729.560 Z=137.150 Rotation: P=0.000000 Y=54.806927 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=13
CreatureBat_C
Translation: X=564.705 Y=1553.270 Z=27.150 Rotation: P=0.000000 Y=34.152084 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=0
CreatureBat_C
Translation: X=724.428 Y=1631.911 Z=27.150 Rotation: P=0.000000 Y=-71.286896 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=1
CreatureSmallSpider_C
Translation: X=1154.177 Y=1598.896 Z=32.150 Rotation: P=0.000000 Y=47.967991 R=0.000000 Scale X=4.000 Y=4.000 Z=4.000
ID=2,HP=45,Sleep=true
CreatureSmallSpider_C
Translation: X=802.849 Y=1645.774 Z=32.150 Rotation: P=0.000000 Y=83.009689 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=3
CreatureSmallSpider_C
Translation: X=827.667 Y=1970.117 Z=32.150 Rotation: P=0.000000 Y=44.411091 R=0.000000 Scale X=4.000 Y=4.000 Z=4.000
ID=4,HP=40,Sleep=true
CreatureSmallSpider_C
Translation: X=483.923 Y=1953.216 Z=32.150 Rotation: P=0.000000 Y=123.319824 R=0.000000 Scale X=1.000 Y=1.000 Z=1.000
ID=5
```