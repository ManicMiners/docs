# Reserved Words
List of keywords in alphabetical order used by the script engine. These should not be used by variable names or event chains.  Doing so will have undefined behavior!

|Name|Type|Brief Description|
|---|---|---|
|A|Emerge Direction|Automatic.|
|addrandomspawn|Event|Config random spawn.|
|air|Macro|Air remaining.|
|arrow|Variable|Arrow object.|
|Barrier_C|Collection|TODO what are these?|
|black|Color|Arrow colors.|
|blue|Color|Arrow colors.|
|bool|Variable|true false.|
|building|Variable|Building object (different use than building trigger).|
|building|Class Trigger|Building Trigger (different use than building variable).|
|building_path|Macro|Tile ID of a building path (14).|
|BuildingDocks_C|Collection|Docks|
|BuildingElectricFence_C|Collection|The fence item and fence building are two separate objects|
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
|Crystal_C|Collection|All crystals include those needing recharge.|
|crystal_seam|Macro|Tile ID of a crystal seam (42).|
|crystals|Macro|Crystal count.|
|darkgreen|Color|Arrow colors.|
|dead|Data Field Trigger|Trigger when object is dead.|
|dirt|Macro|Tile ID of dirt (26).|
|drill|Event|Drill tile.|
|driven|Data Field Trigger|Trigger when a miner enters a vehicle.|
|driver|Data Field|miner id of the driver. Same as driverid.|
|driverid|Data Field|miner id of the driver. Same as driver.|
|Dynamite_C|Collection|All dynamite outside of toolstore.|
|E|Emerge Direction|East.|
|eaten|Data Field|The number of crystals eaten/absorbed.|
|ElectricFence_C|Collection|All fence objects.|
|emerge|Event|Spawn creature.|
|EventErosion_C|Collection|Active erosions.|
|EventLandslide_C|Collection|Active active landslides.|
|erosionscale|Macro|Global erosion scale factor|
|float|Variable|Floating point number.|
|get|Macro|Get tile ID.|
|green|Color|Arrow colors.|
|hard_rock|Macro|Tile ID of hard rock (34).|
|heal|Event|Heal object.|
|hostiles|Macro|Number of hostile creatures.|
|health|Data Field|Object hitpoints. Same has hp.|
|hp|Data Field|Object hitpoints. Same has health.|
|hurt|Data Field Trigger|Trigger when object takes damage.|
|id|Data Field|Object ID.|
|if|Trigger|single time trigger.|
|init|Event Chain|First event called after map load.|
|intarray|Variable|Integer array.|
|integer|Variable|Integer number.|
|ispowered|Data Field|Same as power.|
|kill|Event|Kill object.|
|lastbuilding|Macro|Last building that activated a trigger.|
|lastcreature|Macro|Last creature that activated a trigger.|
|lastminer|Macro|Last miner that activated a trigger.|
|lastvehicle|Macro|Last vehicle that activated a trigger.|
|lava|Macro|Tile ID of lava (6).|
|level|Data Field|Returns upgrade level of the building.|
|loose_rock|Macro|Tile ID of loose rock (30).|
|lose|Event|Lose the map.|
|miner|Variable|Miner object (different use than miner triggers).|
|miner|Class|miner class in triggers (different use than miner variable).|
|miners|Macro|Miners discovered or active.|
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
|ore_seam|Macro|Tile ID of an ore seam (46).|
|pan|Event|Pan camera.|
|place|Event|Change tile.|
|power|Data Field|Returns 1 if the building has power, 0 if it doesn't.|
|powered|Data Field|Same as power.|
|poweroff|Data Field Trigger|Trigger when power is deactivated for a building.|
|poweron|Data Field Trigger|Trigger when power is activated for a building.|
|progress_path|Macro|Tile id of a progress path (13).|
|qmsgs|Event|Display message to user.|
|RechargeSeamGoal_C|Collection|Visible recharge seams.|
|red|Color|Arrow colors.|
|row|Data Field|Object row.|
|S|Emerge Direction|South.|
|save|Event|Save last miner that activated a trigger into a variable.|
|savebuilding|Event|Save last building that activated a trigger into a variable.|
|shake|Event|Shake camera.|
|slug_hole|Macro|Tile id of slimy slug hole (12).|
|slugs|Macro|Number of slimy slugs.|
|solid_rock|Macro|Tile ID of solid rock (38).|
|sound|Event|Play .ogg file.|
|spawncap|Event|Config random spawn.|
|spawnwave|Event|Config random spawn.|
|stamina|Data Field|same as hp.|
|startrandomspawn|Event|Start configured random spawn.|
|starttimer|Event|Start a timer.|
|stoprandomspawn|Event|Stop random spawn.|
|stoptimer|Event|Stop a timer.|
|Stud_C|Collection|All building studs.|
|studs|Macro|Building Stud count.|
|string|Variable|Text.|
|tick|Event Chain|Called on every engine tick. Not recommended.|
|tile|Data Field|TileID for objectt.|
|tileid|Data Field|same as tile.|
|time|Macro|Game time.|
|timer|Variable|Timer object.|
|truewait|Event|Suspend event chain for real user time period.|
|upgraded|Trigger when object is upgraded.|
|vehicle|Variable|Vehicle object (different use than miner triggers).|
|vehicle|Class|Vehicle class in trigger (different use than vehicle variable).|
|vehicles|Macro|Number of vehicles.|
|wait|Event|Suspend event chain for a given period of time modified by game speed.|
|water|Macro|Tile ID of water (11).|
|W|Emerge Direction|West.|
|when|Trigger|multiple time trigger.|
|white|Color|Arrow colors.|
|win|Event|Win the map.|
|X|Data Field|Column, 300 values per cell|
|Y|Data Field|Row, 300 values per cell|
|yellow|Colors|Arrow colors.|
|Z|Data Field|Height, 300 values per cell|

