# DAT Section briefing

The briefing section may be filled in with lines of text that are displayed to the player prior to starting the map.

Generally the player would expect that this text would provide some sort of useful information about the map, but the map designer is free to use this text to display to the user whatever they feel is important.

Each line of text is considered a paragraph, auto-wrapping to fit inside of the dialog box. Every line in this section is part of the displayed text.

There is no known limit on the size of this section, the player is given a scrollable dialog box to read the text.

Use of the keyword `CADET` (upper case) will be automatically filled in with the players name when the dialog is displayed.

Example:

```
briefing{
Get ready CADET - this is going to be a hard mission. A remote base was trapped in a cavern by landslides, but before we lost contact with them they were also under threat from rising lava.

Scans have found a reasonably safe location from the lava where we will transport you into - but they also indicate nearby monsters.

Your mission - quickly build up a base, defend it and use the tunnel scout to locate the remote base and power it back up so everyone may be safely teleported back to the ship before the rising lava engulfs the cavern.

Good luck CADET.
}
```

>The message may contain non-ANSI characters. If any are used, the editor will save the map using UTF16LE BOM format.