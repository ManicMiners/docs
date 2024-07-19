# Timers

Periodic timers are created by either the visual block system or use of a timer variable. Once a timer is created, it will continue to fire on the given interval until the user exits the map or stoptimer event is used.

When the game is paused, timers are suspended.

 The interval values may be floating point numbers and the engine does support sub second timings. Naturally as timers fire faster or the more timers are active - internal overhead associated with them increases. That said, using timers is always more efficient than using the `tick` Event Chain.

Timers are controlled by a timer variable

```mms
timer MyTimer=DELAY,MIN,MAX,EVENTCHAIN
```

Defines a variable of type timer with the given name MyTimer. It will wait delay seconds to start, and will fire between min seconds and max seconds after the last firing, calling the given eventchain. Timer values may be int or float.

See Levels\DEMO\Scripts\demotimers.dat for examples.

Using a timer variable allows use of `stoptimer` and `starttimer` events.

|Syntax|Description|
|---|---|
|starttimer:name|name is timer variable, its timer is started if it was stopped.|
|stoptimer:name|name is a timer variable, its timer is stopped if it is running.|

Timers continue to fire even after losing the game. If you are manually controlling the win/lose cases, it may be a good idea to use stoptimer on any active timers when the player loses the map.

After wining the map, players may decide to continue to play and the timers will continue to fire. You may need to account for this to prevent any map lose messages after winning.

timers are not real variables. They cannot be assigned to each other nor used in any context other than the two events above.