# Classes and Collections

The various objects in the game are usually associated with a class and/or collection. A collection is a wrapper for  multiple similar objects. Most Classes and Collections may be used with triggers to get notification related to that class or with conditions to test values in comparisons.

Currently classes can be divided in the following subcategories:

- [Arrows](_pages/ClassesArrow)
- [Buildings](_pages/ClassesBuildings)
- [Creatures](_pages/classesCreatures)
- [Miners](_pages/ClassesMiners)
- [Timers](_pages/ClassesTimer)
- [Vehicles](_pages/ClassesVehicles)
- Environmental Collections

## Environment Collections

Environment Collections are special collections that are read only and are used as a macro, returning the number of discovered objects of that type. These collections do not have properties. TODO RESEARCH if any properties work.

|Name|Description|
|---|---|
|Barrier_C|TODO.|
|Crystal_C|Number of energy crystals active not yet stored. It is the number of green/purple ones on the ground and those being carried by miners or vehicles. Does not include any eaten by monsters.|
|Dynamite_C|Number of dynamite outside of toolstore. They can be carried by a miner or dropped on the ground.|
|ElectricFence_C|Number of electric fences placed on the map. TODO does it includes ones being carried?|
|EventErosion_C|Number of ongoing erosions.|
|EventLandslide_C|Number of ongoing landslides.|
|NavModifierLava_C |Amount of lava tiles.|
|NavModifierPowerPath_C|Amount of Power Path tiles, any type. Only finished paths.|
|NavModifierRubble_C|Amount of Rubble tiles, any stage.|
|NavModifierWater_C|Amount of water tiles.|
|Ore_C|Number of Ore collected.  Can be changed by assigning **ore** macro with a new value.|
|RechargeSeamGoal_C|Number of discovered recharge seams.|
|Stud_C|Number of Studs collected. Can be changed by assigning **studs** macro with a new value.|


