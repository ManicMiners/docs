# Event chains
You can declare multiple events as chains (functions) that can be executed all at once.

!> When using event chains *occurrance* `when/if` must be omitted.

```mms
	# You can write it like this...
	EVENT_CHAIN::EVENT;
	EVENT;
	EVENT; 

	#...or like this
	EVENT_CHAIN::;
	EVENT;
	EVENT;
```

- You can use whatever name you want instead of EVENT_CHAIN except for those already taken by macros.
- The `EVENT` events will execute in order as they are written.

!> After each event chain there must be an **empty line** to signal the end of the chain.

When you write a name that refer to a event chain instead of a regular event it will call the event chain and execute the events one by one. This can occur multiple times. You can put delays in event chains using the `wait` event, at which point the rest of the event will execute at a later time.

## Init
The Init or Initialize event chain runs before any trigger can occurr in the level. This can be used to setup variables which need modification at runtime. The syntax is the same as any other event chain but the chain name must be Init.

```mms
	init::doStuff;
```

## Conditions
Conditions can also be used together with event chains. They can be used with one or **optionally** two events.

```mms
	EVENT_CHAIN::EVENT;
	((CONDITION))[EVENT_TRUE][EVENT_FALSE];
```

The above statement fire `EVENT_TRUE` if ``((CONDITION))`` equals `true` or `EVENT_FALSE` if it equals `false`
## Example

```mms
	int counter=0	#A number
	string myStr="Counter: "	#A partial message
	string myMsg	#A blank string

	if(time:5)[myChain]	#A trigger
	
	myChain::;	#The Chain
	counter+=1;	#Increase the counter
	myMsg=myStr+counter;	#Combine a message
	msg:myMsg;	#Display the message
```
	
The above code run after 5 game-seconds, increases the counter from 0 to 1 and display a message to the player.