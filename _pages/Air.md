# Air

There are two types of maps in relationship with air.
- maps with no air requirement. Miners do not use air.
- maps with air requirement. Miners use air.

Use of the `oxygen:` key in the info section determines what kind of air map. If the key is missing, you have no air requirement. If the key is present, then the map has an air requirement.

Maps with no air requirement act as if the there is an oxygen:6000/6000 statement but miners do not use any air. Thus the map always has 6000 air.

Maps with an air requirement start with an initial value of oxygen and have a maximum amount of oxygen. This is defined in the info section via the `oxygen:` keyword. If air drops to 0, the player loses the game.

Facts about air:
- Miners consume one air per second. Thus 100 air is able to support one miner for 100 seconds, or ten miners for ten seconds.
- Support Stations each generate ten air per second. Thus each Support Station may support ten miners indefinitely.
- Discovering a cavern will start returning ten air per floor tile discovered. This air is returned over time, no more than 100 air per second is returned.
- Script has a air macro - this allows direct modification of air. This works in both types of maps!
- air can never be less than zero. If zero, the player loses the map.

> Even if air goes to 0 in a no air requirement map (by using script), the player never loses the game. 

## air macro in script

Scripting has the `air` read/write macro. It allow direct and immediate change to the air in the cavern. If adding air, the air instantly is updated - it is not added over time. Air will always be capped to the maximum air amount set in the info section `oxygen:` keyword. Air cannot be less than 0, any attempt to set air to a negative value is automatically set to 0. Setting air to 0 will cause the player to lose the map.

Script examples with air
```
air+=100;   # adding 100 air to cavern
air=2000;   # force air to this specific value
```

Since `air` is a macro it can be used in triggers and conditionals.

```
if(air<200)[msg:msgLowAir]   # one time trigger if air is lower than 200

EventChainAddAirIfLow::;
((air<200))air+=20;     # give some air if too low allowing player to live longer

