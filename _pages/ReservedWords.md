# Reserved Words
List of keywords in alphabetical order used by the script engine. These should not be used as variable names or event chain names.  Doing so will have undefined behavior!
These are not case sensitive since variable names and event chain names are not case sensitive.

|Name|Type|Brief Description|
|---|---|---|
|A|Emerge Direction|Automatic.|
|addrandomspawn|Event|Config random spawn.|
|air|Macro|Air remaining.|
|arrow|Variable|Arrow object.|
|Barrier_C|Collection|Construction barriers released from toolstore|
|Bat|Collection|Bats.|
|Bat_C|Collection|Bats.|
|black|Color|Arrow colors.|
|blue|Color|Arrow colors.|
|bool|Variable|true false.|
|building|Variable / Class Trigger|Building object or trigger.|
|building_path|Macro|Tile ID of a building path (14).|
|BuildingCanteen_C|Collection|Canteen|
|BuildingDocks_C|Collection|Docks|
|BuildingElectricFence_C|Collection|Electric Fences.|
|BuildingGeologicalCenter_C|Collection|Geological Centers|
|BuildingMiningLaser_C|Collection|Mining Lasers|
|BuildingOreRefinery_C|Collection|Ore Refineries|
|BuildingPowerPath_C|Collection|Building power paths in progress.|
|BuildingPowerStation_C|Collection|Power Stations|
|buildings|Macro|Number of buildings.|
|BuildingSuperTeleport_C|Collection|Super Teleports|
|BuildingSupportStation_C|Collection|Support Stations|
|BuildingTeleportPad_C|Collection|Teleport Pads|
|BuildingToolStore_C|Collection|Toolstores|
|BuildingUpgradeStation_C|Collection|Upgrade Stations|
|built|Data Field Trigger|Trigger when a building is built.|
|canteen|Macro|Number of Canteens.|
|Canteen_C|Macro|Number of Canteens.|
|cargocarrier|Macro|Number of Cargo Carriers.|
|CargoCarrier_C|Macro|Number of Cargo Carriers.|
|change|Trigger|Trigger when tile changes|
|chromecrusher|Macro|Number of Chrome Crushers.|
|ChromeCrusher_C|Macro|Number of Chrome Crushers.|
|click|Data Field Trigger|Trigger when object is clicked.|
|clock|Macro|Same as time.|
|col|Data Field|Object column. Same as column.|
|column|Data Field|Object column. same as col.|
|ConstructedBuilding|Macro|Last constructed building.|
|creature|Variable|Creature object.|
|CreatureBat_C|Collection|Bat objects.|
|CreatureIceMonster_C|Collection|Ice monster objects.|
|CreatureLavaMonster_C|Collection|Lava monster objects.|
|CreatureRockMonster_C|Collection|Rock monster objects.|
|CreatureSmallSpider_C|Collection|Spider objects.|
|CreatureSlimySlug_C|Collection|Slimy Slug objects.|
|creatures|Macro|Number of creatures.|
|Crystal_C|Collection|Unstored crystals include those needing recharge.|
|crystal_seam|Macro|Tile ID of a crystal seam (42).|
|crystals|Macro|Stored Crystal count.|
|darkgreen|Color|Arrow colors.|
|dead|Data Field Trigger|Trigger when object is dead.|
|dirt|Macro|Tile ID of dirt (26).|
|disable|Event|Disable object.|
|discovertile|Objective|Objective section keyword.|
|docks|Macro|Number of Docks.|
|Docks_C|Macro|Number of Docks.|
|drill|Event / Trigger|Drill tile.|
|drive|Trigger|Trigger when vehicle over tile.|
|driven|Data Field Trigger|Trigger when a miner enters a vehicle.|
|driver|Data Field|miner id of the driver. Same as driverid.|
|driverid|Data Field|miner id of the driver. Same as driver.|
|Dynamite_C|Collection|All dynamite outside of toolstore.|
|E|Emerge Direction|East.|
|eaten|Data Field|The number of crystals eaten/absorbed.|
|electricfence|Macro|Number of Fences.|
|ElectricFence_C|Macro|Number of Fence objects. Not a collection.|
|emerge|Event|Spawn creature.|
|enable|Event|Enable object|
|enter|Trigger|Trigger when object enters tile.|
|EventErosion_C|Collection|Active erosions.|
|EventLandslide_C|Collection|Active active landslides.|
|erosionscale|Macro|Global erosion scale factor|
|false|boolean|bool false or numeric 0.|
|findbuilding|Objective|Objective section keyword.|
|float|Variable|Floating point number.|
|geologicalcenter|Macro|Number of Geological Centers.|
|GeologicalCenter_C|Macro|Number of Geological Centers.|
|get|Macro|Get tile ID.|
|granitegrinder|Macro|Number of Granite Grinders.|
|GraniteGrinder_C|Macro|Number of Granite Grinders.|
|green|Color|Arrow colors.|
|hard_rock|Macro|Tile ID of hard rock (34).|
|heal|Event|Heal object.|
|health|Data Field|Object hitpoints. Same has hp.|
|hidearrow|Event|Hide arrow object.|
|highlight|Event|Highlight tile.|
|highlightarrow|[Event]|showarrow and highlight at once.|
|hostiles|Macro|Number of hostile creatures.|
|hover|Trigger|Trigger when mouse is over a tile.|
|hoverscout|Macro|Number of Hover Scouts.|
|HoverScout_C|Macro|Number of Hover Scouts.|
|hp|Data Field|Object hitpoints. Same has health.|
|hurt|Data Field Trigger|Trigger when object takes damage.|
|IceMonster|Collection|Ice Monsters.|
|IceMonster_C|Collection|Ice Monsters.|
|id|Data Field|Object ID.|
|if|Trigger|single time trigger.|
|init|Event Chain|First event called after map load.|
|intarray|Variable|Integer array.|
|integer|Variable|Integer number.|
|ispowered|Data Field|Same as power.|
|kill|Event|Kill object.|
|landslide|Event|Unknown.|
|laser|Trigger|Trigger when wall destroyed by laser.|
|laserhit|Trigger|Trigger when wall hit by laser.|
|lastbuilding|Macro|Last building that activated a trigger.|
|lastcreature|Macro|Last creature that activated a trigger.|
|lastminer|Macro|Last miner that activated a trigger.|
|lastvehicle|Macro|Last vehicle that activated a trigger.|
|lava|Macro|Tile ID of lava (6).|
|LavaMonster|Collection|Lava Monsters.|
|LavaMonster_C|Collection|Lava Monsters.|
|level|Data Field|Returns upgrade level of the building.|
|levelup|Data Field Trigger|Miner or Building upgraded.|
|light|Parameter|enable/disable parameter.|
|lights|Parameter|same as light.|
|LMLC|Macro|Number of Large Mobile Laser Cutters.|
|LMLC_C|Macro|Number of Large Mobile Laser Cutters.|
|loaderdozer|Macro|Number of Loader Dozers.|
|LoaderDozer_C|Macro|Number of Loader Dozers.|
|loose_rock|Macro|Tile ID of loose rock (30).|
|lose|Event|Lose the map.|
|miner|Variable / Class|Miner object or class.|
|miners|Macro|Miners discovered or active.|
|mininglaser|Macro|Number of Geological Centers.|
|MiningLaser_C|Macro|Number of Geological Centers.|
|monsters|Macro|Number of monsters.|
|msg|Event|Display a message to user.|
|N|Emerge Direction|North.|
|NavModifierLava_C |Collection|Amount of lava tiles.|
|NavModifierPowerPath_C|Collection|Amount of Power Path tiles, any type. Only finished paths.|
|NavModifierRubble_C|Collection|Amount of Rubble tiles, any stage.|
|NavModifierWater_C|Collection|Amount of water tiles.|
|new|Data Field Trigger|Trigger when object is created.|
|ore|Macro|Ore count.|
|Ore_C|Collection|All ore.|
|orerefinery|Macro|Number of Ore Refineries.|
|OreRefinery_C|Macro|Number of Ore Refineries.|
|ore_seam|Macro|Tile ID of an ore seam (46).|
|pan|Event|Pan camera.|
|pause|Event|Pauses the game.|
|place|Event|Change tile.|
|power|Data Field|Returns 1 if the building has power, 0 if it doesn't.|
|powered|Data Field|Same as power.|
|poweroff|Data Field Trigger|Trigger when power is deactivated for a building.|
|poweron|Data Field Trigger|Trigger when power is activated for a building.|
|powerstation|Macro|Number of Power Stations.|
|PowerStation_C|Macro|Number of Power Stations.|
|progress_path|Macro|Tile id of a progress path (13).|
|qmsg|Event|Display message to user.|
|random|Macro|Return random number [low,high]. Random(low)(high). Floats allowed
|rapidrider|Macro|Number of Rapid Riders.|
|RapidRider_C|Macro|Number of Rapid Riders.|
|RechargeSeamGoal_C|Collection|Visible recharge seams.|
|red|Color|Arrow colors.|
|reinforce|Trigger|Trigger when wall is reinforced.|
|reset|Event|Resets the player's selection|
|resetspeed|Event|Loads the game speed from settings again.|
|resources|Objective|Objective section keyword.|
|resume|Event|Same as unpause.|
|RockMonster|Collection|Rock Monsters.|
|RockMonster_C|Collection|Rock Monsters.|
|row|Data Field|Object row.|
|S|Emerge Direction|South.|
|save|Event|Save last miner that activated a trigger into a variable.|
|savebuilding|Event|Save last building that activated a trigger into a variable.|
|savecreature|Event|Save last creature that activated a trigger into a variable.|
|savevehicle|Event|Save last vehicle that activated a triggger into a variable.|
|shake|Event|Shake camera.|
|showarrow|Event|Show arrow object.|
|SlimySlug|Collection|Slimy Slugs.|
|SlimySlug_C|Collection|Slimy Slugs.|
|slug_hole|Macro|Tile id of slimy slug hole (12).|
|slugs|Macro|Number of slimy slugs.|
|smalldigger|Macro|Number of Small Diggers.|
|SmallDigger_C|Macro|Number of Small Diggers.|
|SmallSpider|Collection|Small Spiders.|
|SmallSpider_C|Collection|Small Spiders.|
|smalltransporttruck|Macro|Number of Small Transport Trucks.|
|SmallTransportTruck_C|Macro|Number of Small Transport Trucks.|
|SMLC|Macro|Number of Small Mobile Laser Cutters|
|SMLC_C|Macro|Number of Small Mobile Laser Cutters|
|solid_rock|Macro|Tile ID of solid rock (38).|
|sound|Event|Play .ogg file.|
|spawncap|Event|Config random spawn.|
|spawnwave|Event|Config random spawn.|
|speed|Event|Sets the game speed.|
|stamina|Data Field|same as hp.|
|startrandomspawn|Event|Start configured random spawn.|
|starttimer|Event|Start a timer.|
|stoprandomspawn|Event|Stop random spawn.|
|stoptimer|Event|Stop a timer.|
|Stud_C|Collection|All building studs.|
|studs|Macro|Building Stud count.|
|string|Variable|Text.|
|superteleport|Macro|Number of Super Teleports.|
|SuperTeleport_C|Macro|Number of Super Teleports.|
|supportstation|Macro|Number of Support Stations.|
|SupportStation_C|Macro|Number of Support Stations.|
|teleportpad|Macro|Number of Teleport Pads.|
|TeleportPad_C|Macro|Number of Teleport Pads.|
|tick|Event Chain|Called on every engine tick. Not recommended.|
|tile|Data Field|TileID for objectt.|
|tileid|Data Field|same as tile.|
|time|Macro / Trigger|Game time or trigger.|
|timer|Variable|Timer object.|
|toolstore|Macro|Returns number of toolstores.|
|Toolstore_C|Macro|Returns number of toolstores.|
|true|boolean|bool value or 1 as numeric.|
|truewait|Event|Suspend event chain for real user time period.|
|tunnelscout|Macro|Number of Tunnel Scouts.|
|tunneltransport|Macro|Number of Tunnel Transports.|
|TunnelTransport_C|Macro|Number of Tunnel Transports.|
|upgrade|Trigger when vehicle is upgraded.|
|upgraded|Trigger|Not working, don't use.|
|upgradestation|Macro|Number of Upgrade Stations.|
|UpgradeStation_C|Macro|Number of Upgrade Stations.|
|unpause|Event|Resumes the game if paused.|
|variable|Objective|Objective map section.|
|vehicle|Variable / Class|Vehicle object or trigger class.|
|vehicles|Macro|Number of vehicles.|
|VehicleCargoCarrier_C|Collection|Cargo Carriers|
|VehicleChromeCrusher_C|Collection|Chrome Crushers|
|VehicleGraniteGrinder_C|Collection|Granite Grinders|
|VehicleHoverScout_C|Collection|Hover Scouts|
|VehicleLMLC_C|Collection|Large Mobile Laser Cutters|
|VehicleLoaderDozer_C|Collection|Loader Dozers|
|VehicleRapidRider_C|Collection|Rapid Riders|
|VehicleSmallDigger_C|Collection|Small Diggers|
|VehicleSmallTransportTruck_C|Collection|Small Transport Trucks|
|VehicleSMLC_C|Collection|Small Mobile Laser Cutter|
|VehicleTunnelScout_C|Collection|Tunnel Scouts|
|VehicleTunnelTransport_C|Collection|Tunnel Transports|
|wait|Event|Suspend event chain for a given period of time modified by game speed.|
|walk|Trigger|Trigger when miner walks on a tile.|
|water|Macro|Tile ID of water (11).|
|W|Emerge Direction|West.|
|when|Trigger|multiple time trigger.|
|white|Color|Arrow colors.|
|win|Event|Win the map.|
|X|Data Field|Column, 300 values per cell|
|Y|Data Field|Row, 300 values per cell|
|yellow|Colors|Arrow colors.|
|Z|Data Field|Height, 300 values per cell|

## Block system reserved words
The Block system generates internal timer variable names and a number of event chains. The names of these change based on the number of blocks and it is undefined behavior for a developer to rely on any fixed name generated automatically by the block system.

Developers should not use any variable names or event chain names that begin with the following names:

- CreatureEmergeEvent
- FleeTo
- PlaceEvent
- RandomSpawnSetup
- ScriptBlockTimerTrigger
- StartRandomSpawn
- StopRandomSpawn
- TimerTrigger
