# Macros
There exist variable names that are reserved as macros. When used in Scripting, these can return, and in some cases set a value.

## Macros used read-only.

- Macros used in a condition are not modified.
- Macros used as part of an assignment type of math expression on the right hand side are not modified.
- Collections will return the number in the collection.
- Macros that refer to built in counts will return that value.
- Most values are int, but some return float and they are converted automatically to int if the other operands are int.

|Macro|Return Type|Function|
|----|----|----|
|air|int|Returns the air status in miner-seconds.|
|buildings|int|Returns the amount of buildings.|
|building_path|int|Returns tile id of a building path (14).|
|cargocarrier|int|Return number of Cargo Carriers.|
|chromecrusher|int|Return number of Chrome Crushers.|
|clock|float|Returns the amount of seconds that have passed since the level. Same as time.|
|ConstructedBuilding|building|Return the last constructed building.|
|creatures|int|Returns number of creatures.|
|crystals|int|Returns the stored crystal count.|
|Crystal_C|int|Returns the unstored crystal count.|
|crystal_seam|int|Returns tile id of a crystal seam (42).|
|dirt|int|Returns tile id of dirt (26).|
|docks|int|Returns number of Docks.|
|electricfence|int|Returns number of Fences.|
|ElectricFence_C|int|Returns number of fence objects. Not a collection.|
|erosionscale|float|Returns or sets the erosionscale.|
|geologicalcenter|int|Returns number of Geological Centers.|
|get(ROW)(COLUMN)|int|Returns the tile ID of the specified coordinates. ROW COLUMN are ints.|
|granitegrinder|int|Return Number of Granite Grinders.|
|hard_rock|int|Returns tile id of hard rock (34).|
|hostiles|int|Returns number of hostile units.|
|hoverscout|int|Return Number of Hover Scouts.|
|lastbuilding|building|Return the last building that activated a trigger.|
|lastcreature|creature|Return the last creature that activated a trigger.|
|lastminer|miner|Return the last miner that activated a trigger.|
|lastvehicle|vehicle|Return the last vehicle that activated a trigger.|
|lava|int|Returns tile id of lava (6).|
|LMLC|int|Return number of Large Mobile Laser Cutters.|
|loaderdozer|int|Return number of Loader Dozers.|
|loose_rock|int|Returns tile id of loose rock (30).|
|miners|int|Returns the amount of miners.|
|mininglaser|int|Returns number of Geological Centers.|
|monsters|int|Returns number of monsters.|
|ore|int|Returns the ore count.|
|orerefinery|int|Returns number of Ore Refineries.|
|ore_seam|int|Returns tile id of an ore seam (46).|
|powerstation|int|Returns number of Power Stations.|
|progress_path|int|Returns tile id of a progress path (13).|
|random(MIN)(MAX)|int/float|Return random number from MIN to MAX.|
|rapidrider|int|Return number of Rapid Riders.|
|slugs|int|Returns number of slimy slugs.|
|slug_hole|int|Returns tile id of slimy slug hole (12).|
|smalldigger|int|Return number of Small Diggers.|
|smalltransporttruck|int|Return number of Small Transport Trucks.|
|SMLC|int|Return number of Small Mobile Laser Cutters|
|solid_rock|int|Returns tile id of solid rock (38).|
|studs|int|Returns number of building studs.|
|supportstation|int|Returns number of Support Stations.|
|teleportpad|int|Returns number of Teleport Pads.|
|time|float|Returns the amount of seconds that have passed since the level began. Same as clock.|
|toolstore|int|Returns number of toolstores. Similar to BuildingToolStore_C|
|tunnelscout|int|Return number of Tunnel Scouts.|
|tunneltransport|int|Return number of Tunnel Transports.|
|upgradestation|int|Returns number of Upgrade Stations.|
|vehicles|int|Returns the amount of vehicles.|
|water|int|Returns tile id of water (11).|

All collection classes may be used as a macro and they will return an int that is the number of objects in that collection.

[building](_pages/ClassesBuildings), [creature](_pages/ClassesCreatures), [miner](_pages/ClassesMiners) and [vehicle](_pages/ClassesVehicles) classes have data fields that allow querying properties on them and they are also treated as a macro. See each class type for the list of data fields it supports.


## Macros that may be modified

A few macros allow modification which changes game play. These may be used on the left side of an assignment type of event.

|Macro|Assignment Type|Function|
|----|----|----|
|air|int|Set current amount of air. Will be capped between zero and map limit. Setting to low numbers may lose the map.|
|crystals|int|Set amount of crystals collected.|
|erosionscale|float|Set erosion scaling.|
|ore|int|Set amount of ore collected.|
|studs|int|Set number of studs collected.|


### Air

Air is specified in miner seconds. One unit of air is the amount of air a single miner will use every game second. Thus one-hundred will support ten miners for ten game seconds or one miner for one-hundred game seconds.

When air gets to zero - the player loses the map.

Each Support Station will add ten air every game second.


## Examples

```mms	
int CrystalGoal=3
string myMsg=You have collected 3 crystals!
	
if(crystals>=CrystalGoal)(msg:myMsg)
```

The above code make the game display a message once when the player has collected 3 or more crystals.

```mms
AddResources::;   # give player resources
air+=10;
crystals+=20;
ore+=30;
studs+=40;
```
The above Event Chain will add air, crystals, ore and studs to the player.
