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

The one thing the blocks may do that script cannot do is have a back-up. If the first action cannot be performed (a creature cannot be spawned is the only case), then a backup wire may fire an alternative action. Script does not have this ability - there is no way for script to know if an emerge event fails.

Using the blocks system in the editor allows an easy way to visualize triggers and actions those triggers cause. Internally much of the block section is converted into internal event chains and the script engine is used to process events.

It is possible for script to directly call the block system, and the block system can itself call event chains in the script section.

This documentation is not an instruction guide on how to use the block system, but it does document all of the types of entries in the block section. In general apps should just read and restore every line in this section. Reviewing this documentation may assist map developers in understanding how the block system works.

> The block system uses internal event chain names - these are automatically generated as needed by the map editor. None of these are intended for script to call directly - doing so is undefined behavior.

## TODO CREATURE BLOCKS

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
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be active.
- NAME is the internally generated EventChain name that is called by the timer. This name must be unique and subject to the same rules of any EventChain name. Script should never call this event chain.
- DELAY is floating point number of seconds from map load until the first time the trigger will fire.
- MAX is the periodic time to refire the trigger.
- MIN is an optional value and is the minimum time for periodic timer. If specified, the refire time is random between the MIN and MAX.

### Event Chain Block
Event chains blocks define a user EventChain name which allows script to call into the block system. Once called by script, it will then chain to other blocks or creatures based on its connected wires. This is the only event chain name that may be called by script.  Be aware that calling this event chain name triggers connecting wires via a asynchronous system - think of this as invoking a trigger that immediately returns, and the actions from that trigger will eventually happen.

Format:
```
ID/TriggerEventChain:ROW,COL,COOLDOWN,NAME
```
- ID is a unique number assigned by the map editor that represents this trigger.
- ROW,COL are the row and column for the block. The actual coordinates do not matter but it must be in a discovered part of the map at map load time to be active.
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

## TODO WIRE BLOCKS