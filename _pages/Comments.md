# Comments
Comments can be typed directly into the script. They are preceded by the `#` symbol. You can also use this to disable certain script lines.

The game engine ignores everything after the `#` comment character.  When added to a script line, the game engine will also ignore all spaces from the end of the script `;`

If an entire line is to be a comment, the comment character must be the first character. You cannot have spaces in front of it.

Having a comment line after the end of an event chain will not terminate the event chain - you still need a blank line.

```mms
	#This comments out the entire line, which is then ignored by the game.
 
	init::disable:lights;      #This comment does NOT block the event on the same line.

	MyChain::;
	air+=100;    # give player 100 air
	#  comment line does not end event chain but the blank line below does.

	NewChain::;

```