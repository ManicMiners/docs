# Creature Class
The creature class is used to create a reference to a creature. With that reference you can then call on and use triggers and properties exclusive to that creature. You may also refer to a creature collection where you may use triggers connected to every creature of a specific type.

## Declaration

```mms
creature MyMonster=2   # The existing creature of ID 2 is mapped to this variable.
creature MyCreature    # will be assigned later by lastcreature or =.
```
- Creature variables not assigned may later be assigned via `=lastcreature` or `savecreature`.
- Creature variables may be assigned to each other.
- Unassigned creature variables cannot be used in a trigger.
- It is common to use a creature collection class in the trigger and use `=lastcreature` or `savecreature` in an event chain.
- Undiscovered creatures and their triggers are inactive until they are discovered.

>Specifying an id only works on creatures that are part of the map. There is no way to dynamically assign at runtime a creature using the id.

## Properties
These are the class properties specific to creatures.  Properties start with the dot `.` character followed by the name after the object variable or collection name.

## Trigger Properties
>These properties are for use in triggers. They cannot be used in assignments or conditions.

|Name|Description|
|---|---|
|dead|Trigger when a creature gets killed or enters rock.|
|new|Trigger when a creature emerges. Only used with collections.|
|wake|Trigger when a creature wakes up.|

## Properties

>These properties are read-only and are used as a macro, returning a value. They may be used in assignment events on the right side, or in conditions for testing. These cannot be used on collections, they must be used with a specific creature.

|Property|Type|Note|
|---|---|---|
|col|int|Returns column of the creature.|
|column|int|Returns column of the creature. Same as col.|
|eaten|int|The number of crystals eaten/absorbed|
|health|int|Returns current hitpoints. Same as hp.|
|hp|int|Returns current hitpoints. Same as health.|
|id|int|Returns the ID of the creature.|
|row|int|Returns row of the creature.|
|tile|int|TileID the creature is over.|
|tileid|int|same as tile.|
|X|int|Column, 300 values per cell|
|Y|int|Row, 300 values per cell|
|Z|int|Height, 300 values per cell|

## Collections 
Each native creature class has its own collection. When used by itself without a trigger property, it is treated as a read-only macro returning the total number of creatures of that type.  Collections may only use trigger properties.

>Undiscovered creatures are inactive and do not receive triggers until they are discovered.  Creatures cannot be spawned into undiscovered areas.

|Name|Description|
|---|---|
|Bat|Bats.|
|Bat_C|Bats.|
|CreatureRockMonster_C|Rock Monsters.|
|CreatureIceMonster_C|Ice Monsters.|
|CreatureLavaMonster_C|Lava Monsters.|
|CreatureSlimySlug_C|Slimy Slugs.|
|CreatureSmallSpider_C|Small Spiders.|
|CreatureBat_C|Bats.|
|IceMonster|Ice Monsters.|
|IceMonster_C|Ice Monsters.|
|LavaMonster|Lava Monsters.|
|LavaMonster_C|Lava Monsters.|
|RockMonster|Rock Monsters.|
|RockMonster_C|Rock Monsters.|
|SlimySlug|Slimy Slugs.|
|SlimySlug_C|Slimy Slugs.|
|SmallSpider|Small Spiders.|
|SmallSpider_C|Small Spiders.|

> There are multiple names for each creature collection; it is recommended to use the long name for clarity. The short names are legacy.

## Macros
These are not collections. They return the number of objects as an int. They may be used in assignments on the right side or in conditions.

- `creatures` macro returns the number of all creatures.
- `hostiles` macro returns the number of monsters and slugs.

## Spawning a Monster
The `emerge` event will try to spawn a single creature near a given location.
```mms
emerge:ROW,COLUMN,DIRECTION,COLLECTION,DISTANCE
```
- ROW,COLUMN is the tile location to try to spawn the creature.
- Direction is one of `A` automatic, `N` north, `S` south, `E` east, `W` west. This is the direction the monster will attempt to come out. It is best to always use `A` for automatic.
- COLLECTION is the type of creature to spawn. See list of collections above.
- DISTANCE is the number of tiles around the ROW,COLUMN to look for a valid spawn location. 0 means to only spawn from the given tile.  The logs will have a warning if the spawn fails.

Example spawning an Ice Monster from row 5 column 4.
```mms
emerge:5,4,A,CreatureIceMonster_C,0;
```

The `randomspawn` event will try to spawn a single creature anywhere in the discovered area of the map.
```mms
randomspawn:COLLECTION
```

Monsters may only spawn from a valid flat (non-corner), non-reinforced wall that is dirt, loose rock, or hard rock.

With script it is possible to give the appearance that a monster can spawn from other flat walls by changing the wall tile first to something that is spawnable, doing the spawn, then changing it back.

Both single unit spawning and the below automatic monster spawning do not support changing the monster health or scale. Only monsters placed into the map via the map editor may have hp and scale applied to them.

## Automatic Monster Spawning

The following events control automatic pseudo-random monster spawning in waves.

|Event|Description|
|---|---|
|addrandomspawn:COLLECTION,MINTIME,MAXTIME|Configure random spawn of a creature collection. MINTIME and MAXTIME define a random time in float seconds between each spawn wave.|
|spawncap:COLLECTION,MIN,MAX|For the given collection, random spawns will occur until the total number of active creatures is over a random value between MIN and MAX.|
|spawnwave:COLLECTION,MIN,MAX|For the given collection, each spawn wave will have a random number of creatures between MIN and MAX.|
|startrandomspawn:COLLECTION|Start the random spawn for the given collection.|
|stoprandomspawn:COLLECTION|Stop the random spawn for the given collection.|

Although mainly added for slimy slugs, it also works on monsters.  Creatures are spawned on a random basis in waves until the spawncap number of creatures are active. Creatures are spawned from any random valid location in the discovered areas of the map. Valid locations are non-corner, non-reinforced walls of dirt, loose rock, or hard rock.

If you want to have control over the spawn locations, you have to write your own logic using emerge or use the visual block triggers in the map editor.


## Making a creature flee
Use the flee: event to cause a creature to flee to that location.  If you use a collection, all active monsters of that type will flee to that location. The location must be a valid location for the creature; once it gets there, it expects to be able to leave the map as it normally would. Thus, for slimy slugs, it must be a slug hole. For monsters it must be next to a non-corner, non-reinforced wall of dirt, loose rock, hard rock, or solid rock.
>Once creatures are told to flee - they ignore all other `flee` events. If your base is along the path or a vehicle runs across it - they will stop and do normal creature damage. If the creature's fleeing is interrupted by damaging your base, they may ignore the flee point and just exit.

```mms
flee:MyMonster,row,col
flee:CreatureIceMonster_C,row,col
```
In the first example, a specific monster will flee to row,col. 
In the second example, all active ice monsters will flee to row,col.
