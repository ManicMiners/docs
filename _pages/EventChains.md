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

## tick
The tick event chain is called by the engine on EVERY engine tick. It is not recommended to be used unless that action taken by the script is very short. It would be far less overhead to use the block system to create a timer that called script on some useful interval.

```mms
	tick::doSomethingReallyShortAndFast;
```

## Conditions
Conditions can also be used together with event chains. They can be used with one or **optionally** two events.

```mms
	EVENT_CHAIN::EVENT;
	((CONDITION))[EVENT_TRUE][EVENT_FALSE];
	
	#if you only have the true case the syntax drops the []
	((CONDITION))EVENT;
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

## Ending an Event Chain.

A blank line will end an event chain. In fact a trigger or variable statement will also end the event chain but that leaves you with very hard to read code. This means no blank lines (without comment) are allowed in an event chain. To make it easier for you to understand where the event chain ends, just have a blank line.

## return event

The return event will return from the current event chain. It is very useful to return from an event chain from the middle of logic.
```mms
    MyChain::;
	((i<5))return;
	((i>10))return;
	# continuing on will only be if i >=5 and <=10
```

## Looping

There is no traditional looping one would find in other languages. No for, while, until type of loops. There is no goto type of transfer control.
Every use of an event chain from a ((expression))[trueevent][falseevent] is a function call. An example best shows this:
```mms
    int i=0
	int sum=0;
	string s=""

	#loop 5 times
	myChain::i+=1;
	sum+=1;
	((i<5))myChain;  #recursive call to myChain 5 times
	s="Sum: ";
	s+=sum;
	msg:s;
```
Run this example and you get 5 messages printed, all with the sum of 5.  The code after the conditional jump is executed for every iteration of the loop.  This can lead to unexpected results if the coder is not aware that each loop is a subroutine call.

Best practice is to end the event chain after the loop with a blank line. One may need to reorganize your logic to achive this.

The engine has a limit on the number of recursive calls active from any trigger - the total number of recursive event chains is somewhere around 890. Exceeding that may crash the game.
