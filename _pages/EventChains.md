# Event chains
You can declare multiple events as chains (functions) that can be executed all at once. When using event chains `OCCURRANCE`(when/if) must be omitted.

	EVENT_CHAIN::EVENT;
	EVENT;
	EVENT; 
	(EMPTY LINE)

	alternative

	EVENT_CHAIN::;
	EVENT;
	EVENT;
	(EMPTY LINE)


* EVENT_CHAIN is replaced by whatever '''name''' you want to name the event chain.
* EVENT are the events you want to execute, in that order.
* After each event chain there must be an '''empty line''' to signal the end of the chain.
If the event chain calls another event chain, they will not run in parallel. The second event chain will have to finish before the first continues, '''unless the second event chain has a wait event'''.

When you write a name that refer to a event chain instead of a regular event anywhere, it will call the event chain instead and execute the events one by one. This can occur multiple times. You can put delays in event chains using the "wait" event, at which point the rest of the event will execute at a later time.

## Init
The Init (Initialize) event chain runs before any trigger can fire in the level. This can be used to setup variables which need modification at runtime. The syntax is the same as any other event chain but the chain name must be Init.

## Conditions
Conditions can also be used together with event chains. They can be used with one or **optionally** two events.

	EVENT_CHAIN::EVENT;
	((CONDITION))[EVENT_TRUE][EVENT_FALSE];
	
The above statement fire EVENT\_TRUE if CONDITION equals `true` or EVENT\_FALSE if `CONDITION` equals `false`
