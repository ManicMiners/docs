# Macros
There exist variable names that are reserved as macros. When used in Scripting, these can return, and in some cases set a value.

## Macros used read-only.

- Macros used in a condition are not modified.
- Macros used as part of an assignment type of math expression on the right hand side are not modified.
- Collections will return the number in the collection.
- Macros that refer to built in counts will return that value.
- Most values are int, but some return float and they are converted automatically to int if the other operands are int.
- Two macros have parameters: `get` and `random`. The parameters themselves cannot be another macro that requires parameters (see below)

|Macro|Return Type|Function|
|----|----|----|
|air|int|Returns the air status in miner-seconds.|
|bat|int|Returns number of bats.|
|Bat_C|int|Returns number of bats.|
|buildings|int|Returns the amount of buildings.|
|building_path|int|Returns tile id of a building path (14).|
|cargocarrier|int|Return number of Cargo Carriers.|
|CargoCarrier_C|int|Return number of Cargo Carriers.|
|chromecrusher|int|Return number of Chrome Crushers.|
|ChromeCrusher_C|int|Return number of Chrome Crushers.|
|clock|float|Returns the amount of seconds that have passed since the level. Same as time.|
|ConstructedBuilding|building|Return the last constructed building.|
|creatures|int|Returns number of creatures.|
|crystals|int|Returns the stored crystal count.|
|Crystal_C|int|Returns the unstored crystal count.|
|crystal_seam|int|Returns tile id of a crystal seam (42).|
|dirt|int|Returns tile id of dirt (26).|
|docks|int|Returns number of Docks.|
|Docks_C|int|Returns number of Docks.|
|electricfence|int|Returns number of Fences.|
|ElectricFence_C|int|Returns number of fence objects. Not a collection.|
|erosionscale|float|Returns or sets the erosionscale.|
|false|int|Returns 0. For use only with bools.|
|geologicalcenter|int|Returns number of Geological Centers.|
|GeologicalCenter_C|int|Returns number of Geological Centers.|
|get(ROW)(COLUMN)|int|Returns the tile ID of the specified coordinates. ROW COLUMN are ints.|
|granitegrinder|int|Return Number of Granite Grinders.|
|GraniteGrinder_C|int|Return Number of Granite Grinders.|
|hard_rock|int|Returns tile id of hard rock (34).|
|hostiles|int|Returns number of hostile units.|
|hoverscout|int|Return Number of Hover Scouts.|
|lastbuilding|building|Return the last building that activated a trigger.|
|lastcreature|creature|Return the last creature that activated a trigger.|
|lastminer|miner|Return the last miner that activated a trigger.|
|lastvehicle|vehicle|Return the last vehicle that activated a trigger.|
|lava|int|Returns tile id of lava (6).|
|LMLC|int|Return number of Large Mobile Laser Cutters.|
|LMLC_C|int|Return number of Large Mobile Laser Cutters.|
|loaderdozer|int|Return number of Loader Dozers.|
|LoaderDozer_C|int|Return number of Loader Dozers.|
|loose_rock|int|Returns tile id of loose rock (30).|
|miners|int|Returns the amount of miners.|
|mininglaser|int|Returns number of Mining Lasers.|
|MiningLaser_C|int|Returns number of Mining Lasers.|
|monsters|int|Returns number of monsters.|
|ore|int|Returns the ore count.|
|orerefinery|int|Returns number of Ore Refineries.|
|OreRefinery_C|int|Returns number of Ore Refineries.|
|ore_seam|int|Returns tile id of an ore seam (46).|
|powerstation|int|Returns number of Power Stations.|
|PowerStation_C|int|Returns number of Power Stations.|
|progress_path|int|Returns tile id of a progress path (13).|
|random(MIN)(MAX)|int/float|Return random number from MIN to MAX.|
|rapidrider|int|Return number of Rapid Riders.|
|RapidRider_C|int|Return number of Rapid Riders.|
|slugs|int|Returns number of slimy slugs.|
|slug_hole|int|Returns tile id of slimy slug hole (12).|
|smalldigger|int|Return number of Small Diggers.|
|SmallDigger_C|int|Return number of Small Diggers.|
|smalltransporttruck|int|Return number of Small Transport Trucks.|
|SmallTransportTruck_C|int|Return number of Small Transport Trucks.|
|SMLC|int|Return number of Small Mobile Laser Cutters|
|SMLC_C|int|Return number of Small Mobile Laser Cutters|
|solid_rock|int|Returns tile id of solid rock (38).|
|studs|int|Returns number of building studs.|
|supportstation|int|Returns number of Support Stations.|
|SupportStation_C|int|Returns number of Support Stations.|
|teleportpad|int|Returns number of Teleport Pads.|
|TeleportPad_C|int|Returns number of Teleport Pads.|
|time|float|Returns the amount of seconds that have passed since the level began. Same as clock.|
|toolstore|int|Returns number of toolstores.|
|Toolstore_C|int|Returns number of toolstores.|
|true|int|Returns 1. For use only with bools.|
|tunnelscout|int|Return number of Tunnel Scouts.|
|TunnelScout_C|int|Return number of Tunnel Scouts.|
|tunneltransport|int|Return number of Tunnel Transports.|
|TunnelTransport_C|int|Return number of Tunnel Transports.|
|upgradestation|int|Returns number of Upgrade Stations.|
|UpgradeStation|int|Returns number of Upgrade Stations.|
|vehicles|int|Returns the amount of vehicles.|
|water|int|Returns tile id of water (11).|

All collection classes may be used as a macro and they will return an int that is the number of objects in that collection.

[building](_pages/ClassesBuildings), [creature](_pages/ClassesCreatures), [miner](_pages/ClassesMiners) and [vehicle](_pages/ClassesVehicles) classes have data fields that allow querying properties on them and they are also treated as a macro. See each class type for the list of data fields it supports.

## true false booleans.
`true` and `false` are not really macros but are boolean numeric constants. false evaluates to 0 and true evaluates to 1.  While they can be used with int and float values, it is poor programming practice to do so. boolean values should only be used with bool variables.

## Macros that may be modified

A few macros allow modification which changes game play. These may be used on the left side of an assignment type of event.

|Macro|Assignment Type|Function|
|----|----|----|
|air|int|Set current amount of air. Will be capped between zero and map limit. Setting to low numbers may lose the map.|
|crystals|int|Set amount of crystals collected.|
|erosionscale|float|Set erosion scaling.|
|ore|int|Set amount of ore collected.|
|studs|int|Set number of studs collected.|


### erosionscale

erosionscale is initially set to the value in the info section erosionscale key. This value is a multiplier on the time durations. By default 1.0, setting 2.0 will double the length of time for erosion. Changing this value in script will not change the time for the current phase of an erosion but it will be used when the tile transitions to the next phase. It does not appear to affect the delay (TODO need to verify), only the per phase interval.

Setting to 0.0 will cause any future erosion to stop, and any current erosions will move to lava. Once set to 0, erosions will never restart even if you change it to back to any other non-zero value, the engine treats it as a global stop erosions for the remainder of the map.

### Air

[Click here for information about air](_pages/Air).

## Nested parameter macros not allowed.
Two macros require parameters:

|Name|Brief Description|
|---|---|---|
|get(row)(col)| row and col are integers for a row and column in the map, returns tile at that row,col |
|random(low)(high)| returns random number from [low,high], low and high are inclusive.

The parameters cannot be another macro that requires parameters. For example, if you wanted to return a random tile from a 32x32 map - you `cannot` do this:

```mms
mytile=get(random(0)(31),random(0)(31));   # BAD not allowed
```

Nested parameters are not allowed. To do the above you have to compute the row and column first - saving values into int's and use those ints.

```mms
int myrow=0
int mycol=0

MyChain::;
myrow=random(0)(31);        # get random row
mycol=random(0)(31);        # get random col
mytile=get(myrow)(mycol);   # this works.
```

int arrays have the same limitation - array indexes cannot be another array.

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
