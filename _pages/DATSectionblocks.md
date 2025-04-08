# DAT Section blocks

The blocks section describes a visual trigger/action used by the editor that is integrated into the script engine. The editor writes this section on every save. 

The following types of blocks are available:
- Creatures
- Events
- Trigger
- Wires

Triggers by themselves do not do anything, they must be connected by wires to either events or creatures to perform some action. Think of wires just connecting a trigger to an action. Every trigger may have as many wires leaving it as needed. Events may chain to other events or Creatures. The end results are:
- A tile is drilled.
- A tile is placed.
- A Creature is spawned.

The entire block system at map load time is converted into a number of internal event chains. Everything done by the block system is done internally by script. This includes the failed emerge event. The advantage of the block system is that it hides the complexity of script and visually presents triggers and events.

It is possible for script to directly call the block system, and the block system can itself call event chains in the script section.

This documentation is not an instruction guide on how to use the block system, but it does document all of the types of entries in the block section. In general apps should just read and restore every line in this section. Reviewing this documentation may assist map developers in understanding how the block system works.

> The block system uses internal event chain names - these are automatically generated as needed by the map editor. None of these are intended for script to call directly - doing so is undefined behavior.

## Creature Blocks
Creature blocks define what creature and where they will spawn. It also control where they flee to and setups spawning of waves.
There are 5 types of creature blocks:
- Emerge blocks.
- Flee blocks
- Random spawn setup
- Random spawn start
- Random spawn stop

### Emerge Creature Block
This defines the emerge location and type of creature to emerge. It is similar to the script emerge: event but it includes a cooldown.

The format is:
```
ID/EventEmergeCreature:ROW,COL,DIRECTION,COOLDOWN,COLLECTION,RADIUS
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be active.
- DIRECTION is one of `N` `S` `E` `W` `A`. These are North, South, East, West and Automatic. This is the direction the creature is facing after emerging. Using Automatic is recommended.
- COOLDOWN is a floating point number of seconds that must pass between each call. If non-zero, that number of seconds must pass before another call will have any action. Calls are not queued during the cool down period, they are ignored.
- COLLECTION is one of the creature collection classes, see below.
- RADIUS is the number of tiles from ROW,COL where the creature may emerge from - the actual tile used is random if there are multiple tiles in that radius.

The supported creatures are:
- CreatureIceMonster_C
- CreatureLavaMonster_C
- CreatureRockMonster_C
- CreatureSlimySlug_C
- CreatureSmallSpider_C

>Emerge is the only block that if it fails, will use the backup wires.

### Flee Creature Block
This block commands the last emerged creature to flee to a location. It must in some sequence of wires be connected to the block that emerged the creature. It is similar to the script flee: event.

The format is:
```
ID/EventUnitFlee:ROW,COL,ANYWHERE
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column to flee to. It must be a valid location for the creature to exit the map.
- ANYWHERE is boolean. `true` to command the creature to flee to any valid location on the map, `false` to only flee to the given ROW,COL.

### Creature Random Spawn Setup Block
This block defines the creature type and parameters for the random waves of creature spawning. It is a combination of the `addrandomspawn`, `spawncap` and `spawnwave` script events.

Format is:
```
ID/EventRandomSpawnSetup:ROW,COL,COLLECTION,MAXCOOLDOWN,MINCOOLDOWN,MINSPAWN,MAXSPAWN,MINWAVE,MAXWAVE
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be active.
- COLLECTION is one of the creature collection classes, see below.
- MAXCOOLDOWN is the longest time before the next wave will spawn
- MINCOOLDOWN is the shortest time before the next wave will spawn
- MINSPAWN is the minimum number of creatures spawned per wave.
- MAXSPAWN is the maximum number of creatures spawned per wave.
- MINWAVES is the minimum number of waves allowed at any time.
- MAXWAVES is the maximum number of waves allowed at any time.

The supported creatures are:
- CreatureIceMonster_C
- CreatureLavaMonster_C
- CreatureRockMonster_C
- CreatureSlimySlug_C
- CreatureSmallSpider_C

Each collection class MUST have a setup block before waves may be started. The start block does not need to be connected by wires to the setup block, but the setup block must have been executed as some point prior to executing the start/stop blocks.

### Creature Random Spawn Start Block.
This block will enable the previously setup block for the given creature class to start wave generation based on the parameters defined in the setup block. It is similar to the script startrandomspawn event.

Format is:
```
ID/EventRandomSpawnStart:ROW,COL,COLLECTION
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map in order to start the wave processing based on the setup block.
- COLLECTION is one of the creature classes that have a setup block.

The setup block must have been executed prior to this block.


### Creature Random Spawn Stop Block.
This block will enable the previously started block for the given creature class to stop wave generation based on the parameters defined in the setup block. It is similar to the script stoprandomspawn event.

Format is:
```
ID/EventRandomSpawnStop:ROW,COL,COLLECTION
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map in order to stop the wave processing based on the setup block.
- COLLECTION is one of the creature classes that have a setup block and has executed a start block

The setup block and the start block must both have been executed prior to this block.

## Event Blocks
There are 4 types of event blocks:
- Call Event
- Drill
- Place
- Relay

### Event Call Event Block
This block will call the specified event entered by the user. The even can be any script event or an EventChain. The most common use for this is to provide a way for your script to be called by the block system. The event chain will be called asynchronously so the block system does not wait for your event to return before continuing processing wires.

The event chain name you provide will be scheduled to be called just as if some sort of trigger called that event.  

```
ID/EventCallEvent:ROW,COL,COOLDOWN,NAME
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be active.
- COOLDOWN is a floating point number of seconds that must pass between each call. If non-zero, that number of seconds must pass before another call will have any action. Calls are not queued during the cool down period, they are ignored.
- NAME is a user defined name that must be unique and follow the same rules as all event chain names. This name once entered by the user will not change, and it is the event chain name called by the block system into your script.  NAME may also be any single event script command, for example 'win' can be used to win the map.

### Event Drill Block

This will cause the given tile to be drilled. Any wall type of tile will be turned into rubble, which may cause other tiles to also collapse. It is identical to using the script drill event.

```
ID/EventDrill:6,2
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the tile to drill. If the tile is already a ground tile, nothing happens. 

### Event Relay Block

This event itself does not perform any action, but it can be used to chain via wires to other blocks. It has both a cooldown and a delay. Cooldown is the time between activations, activates are ignored until the cooldown from the last activation has passed.
Delay is separate, one activated it will wait that number of seconds and then pass the event to the connected wires.
```
ID/EventRelay:ROW,COL,COOLDOWN,DELAY
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be active.
- COOLDOWN is a floating point number of seconds that must pass between each call. If non-zero, that number of seconds must pass before another call will have any action. Calls are not queued during the cool down period, they are ignored.
- DELAY is an optional floating point number and is how long in seconds once activated to wait to pass on the event to all connected wires.

A example use for this block would be if you want a trigger to have multiple events but at different times. Driving over a tile could cause a monster to spawn a few seconds later, and then later still cause a wall to collapse or a different monster to spawn. That would take two relay blocks with different delay times.

Another advanced use of this block would be to provide to script a way to delay actions without having to write all the timer logic yourself. You could have a `Trigger Event Chain Block` wired to a `Event Relay Block` with a delay value wired to an `Event Call Event Block`. Thus your script would call - causing a delay to start - and later your script is called back after the delay.

### Event Place Block
This event block is identical to the place script event. It allows the abiliity to change the TileID of any single tile.

```
ID/EventPlace:ROW,COL,COOLDOWN,TileID
```
- ID is a unique number assigned by the map editor that represents this event.
- ROW,COL are the row and column for tile to be changed.
- COOLDOWN is a floating point number of seconds that must pass between each call. If non-zero, that number of seconds must pass before another call will have any action. Calls are not queued during the cool down period, they are ignored.
-TileID is the new TileID to assign to the ROW,COL tile.

Just like the script place event, only a single tile is changed. The engine will queue up changes so one is able to construct walls.

## Trigger Blocks

Trigger blocks are those that cause action to be taken. They are similar to `when` statements in script.
The types of triggers are:

- Timers
- Event Chains callable from script.
- Enter a tile.
- Change a tile.

### Timer Block
Timer blocks define a periodic timer that will call blocks connected by wires to it. These are similar to creating a timer variable in script.

Format:
```
ID/TriggerTimer:ROW,COL,NAME,DELAY,MAX,MIN
```

- ID is a unique number assigned by the map editor that represents this trigger.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but the timer is only active once the ROW,COL is discovered.
- NAME is the Timer object generated. This name must be unique and subject to the same rules of any timer variable name.  The map editor by default creates this name but the user is able to edit it in the map editor. Once the name is set, it will not change as long as this block exists.  Script is able to access this timer object in the stoptimer: and starttimer: events.
- DELAY is floating point number of seconds from map load until the first time the trigger will fire.
- MAX is the periodic time to refire the trigger.
- MIN is an optional value and is the minimum time for periodic timer. If specified, the refire time is random between the MIN and MAX.

>The name in this block does not change once the block is created. Thus script is allowed to access it for use in the stoptimer and starttimer events.

### Event Chain Block
Event chains blocks define a user EventChain name which allows script to call into the block system. Once called by script, it will then chain to other blocks or creatures based on its connected wires. This is the only event chain name that may be called by script.  Be aware that calling this event chain name triggers connecting wires via a asynchronous system - think of this as invoking a trigger that immediately returns, and the actions from that trigger will eventually happen.

Format:
```
ID/TriggerEventChain:ROW,COL,COOLDOWN,NAME
```
- ID is a unique number assigned by the map editor that represents this trigger.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be used.
- COOLDOWN is a floating point number of seconds that must pass between each call. If non-zero, that number of seconds must pass before another call will have any action. Calls are not queued during the cool down period, they are ignored.
- NAME is a user defined name that must be unique and follow the same rules as all event chain names. This name once entered by the user will not change, and it is the event chain name your script may call to cause some action within the block system.

### Enter Block
Enter block define a trigger that fires when any miner, vehicle or optionally creature enters the tile. 

Format:
```
ID/TriggerEnter:ROW,COL,COOLDOWN,BMINERS,BVEHICLES,CLASS
```
- ID is a unique number assigned by the map editor that represents this trigger.
- ROW,COL are the row and column for the Tile to trigger on.
- COOLDOWN is a floating point number of seconds that must pass between each enter. If non-zero, that number of seconds must pass before another call will have any action. Enters are not queued during the cool down period, they are ignored.
- BMINERS is true to allow miners to cause trigger, false to ignore miners.
- BVEHICLES is true to allow vehicles to cause trigger, false to ignore vehicles.
- CLASS is optional value and is the collection class to trigger on. It may be any creature, vehicle, and resource collection class. When that class of an object enters the tile, the trigger will fire.

> This is similar to the script `when(enter:ROW,COL,CLASS)` but has less restrictions and a cool down and allows creatures.

> By default, creatures `will not` trigger this block. You must provide the creature collection class for creatures to trigger this. When you do this, miners and vehicles will not trigger. When using a creature class, you must set BMINERS and BVEHICLES to false.  It is not possible to have a single trigger for miners, vehicles and creatures.


### Change Block
Change block will trigger when the given tile changes or optionally changes to the specified tile.

Format:
```
ID/TriggerChange:ROW,COL,COOLDOWN,TILEID
```
- ID is a unique number assigned by the map editor that represents this trigger.
- ROW,COL are the row and column for the tile that will be changed.
- COOLDOWN is a floating point number of seconds that must pass between each change. If non-zero, that number of seconds must pass before another call will have any action. Changes are not queued during the cool down period, they are ignored.
-TILEID is an optional value and if specified will only trigger when changed to the given TileID.

This is nearly identical to the script `when(change:ROW,COL,ID)` trigger except it has a cooldown.

## Wire Blocks
Wire blocks connect blocks to each other, defining a logical order of execution. Every wire is on its own line, so there is only a single source and a single destination. If a block has three wires leave it, each will have its own wire line.

There are three types of wire blocks:
- Script Wire. Connects one block to another block defining a logical order.
- Backup Wire. If an event block fails to execute (only the emerge event can fail), it defines an alternative wire to be used. It is not used unless an emerge has failed.
- Random Wire. In the set of all random wires exiting a block, only a single one will be randomly followed.

Format is:
```
FROMID TYPE TOID
```
- FROMID is the starting block ID number.
- TYPE is the type of wire, either `-` `~` `?`
- TOID is the destination block ID number.

>There are no spaces in the actual format, they are only used for readability in this doc.

`-` are normal wires, when the FROMID block is executed, it will also cause TOID block to execute.
`~` are backup wires. If the emerge event in the FROMID block fails, it will cause the TOID block to execute. If the emerge block is successful, this wire will not be used.
`?` are random wires. All of the random wires are considered a single set, and randomly just one of them will execute. This happens in addition to the normal wires and backup wires.

Example:
```
8-12
8?9
8?10
8?11
8~13
8~14
```

Block 8 has 5 wires leaving it. Block 12 is a normal wire, so block 12 will be told to execute when block 8 executes. If block 8 is an emerge block, it will only execute block 12 if the emerge is successful.

Blocks 9, 10 and 11 are random wires. Only one of them at random will be executed - even if block 8 is an emerge and fails.

Blocks 13 and 14 are backup wires. If block 8 is an emerge event and the emerge fails, block 12 will not execute, but both blocks 13 and 14 will execute. Blocks 13 and 14 will not execute if the emerge is successful or if block 8 is not an emerge block.

>Random wires execute one of them in addition to what other wires may do.

>Backup wires only execute if the emerge block fails.

The use of the `?` and `~` wires are internally implemented as the `?` and `~` modifiers on an event within an Event Chain. See [Events](_pages/Events)

