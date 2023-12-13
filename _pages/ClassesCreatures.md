# Creature Class
The creature class is used to create a reference to a creature. With that reference you can then call on and use triggers and properties exclusive to that creature. You may also refer to a creature collection where you may use triggers connected to every creature of a specific type.

## Declaration

```mms
creature MyMonster=2   # The existing creature of ID 2 is mapped to this variable.
creature MyCreature    # creature not yet assigned to any specific unit
```
If a creature variable is not initialized to a specific creature, it must be initialized later by savecreature, or = events prior to use. This variable cannot be used in any trigger since it is not known at map startup.

## Triggers

|Name|Description|
|---|---|
|dead|Trigger when a creature gets killed or enters rock.|
|new|Trigger when creature is emerged. TODO TEST.

## Properties

|Property|Type|Note|
|---|---|---|
|col|Integer|Returns column of the creature.|
|column|Integer|Returns column of the creature. Same as col.|
|eaten|Integer|The number of crystals eaten/absorbed|
|health|Integer|Returns current hitpoints. Same as hp.|
|hp|Integer|Returns current hitpoints. Same as health.|
|id||Integer|Returns the ID the creature.|
|row|Integer|Returns row of the creature.|
|tile|Integer|TileID the creature is over.|
|tileid|Integer|same as tile.|
|X|Integer|Column, 300 values per cell|
|Y|Integer|Row, 300 values per cell|
|Z|Integer|Height, 300 values per cell|

## Collections 
Each native creature class has their own collection. When used by itself the collection acts like a macro and returns the total amount of creatures of that type. The collection can be used in triggers.

### List of collections

|Name|
|---|
|CreatureRockMonster_C|
|CreatureIceMonster_C|
|CreatureLavaMonster_C|
|CreatureSlimySlug_C|
|CreatureSmallSpider_C|
|CreatureBat_C|

## Automatic Monster Spawning

The following events control automatic pseudo random monster spawning in waves.
| Event | Description |
|-------|-------------|
|addrandomspawn:COLLECTION,MINTIME,MAXTIME|Configure random spawn of a creature collection. MINTIME and MAXTIME define a random time in float seconds between each spawn wave.|
|spawncap:COLLECTION,MIN,MAX|For the given collection, random spawns will occur until total number of active creatures is over a random value between MIN and MAX.|
|spawnwave:COLLECTION,MIN,MAX|For the given collection each spawn wave will have a random number of creatures between MIN and MAX.|
|startrandomspawn:COLLECTION|Start the random spawn for the given collection.|
|stoprandomspawn:COLLECTION|Stop the random spawn for the given collection|

Mainly added for slimy slugs, it work on monsters also.  Creatures are spawned on a random basis in waves until the the spawncap number of creatures are active. Creatures are spawned from any random valid emergeable location in the discovered areas of the map.

If you want to have control over the spawn locations, you have to write your own logic using emerge or use the visual block triggers in the map editor.

Emerge event will allow you the ability to emerge a single creature from a given location and an optional radius

### Making a creature flee
Use the flee: event to cause a creature to flee to that location.  If you use a collection, all active monsters of that type will flee to that location. The location must be a valid location for the creature, once it gets there it expects to be able to leave the map as it normally would. Thus for slimy slugs, it must be a slug hole. For monsters it must be next to a wall that is emergeable or solid rock.

```mms
flee:MyMonster,row,col
flee:CreatureIceMonster_C,row,col
```
First is a specific monster will flee to row,col
Second is all active ice monsters will flee to row,col.