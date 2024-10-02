# DAT Section comments

The comment section is a section that is not modified by the map editor. It is for any purpose and there is no specification on how it is intended to be used.

The map editor will read each line in this section and write out those lines when the map is saved without any modification. When a new map is created, this section is empty.

In general this section is for use by external DAT utilities.

While there is no specification on how this section is to be formatted, it is generally understood that external utilities would look in this section for data they have written before and ignore any data that was not part of that utility.

To easily support any external utility, it is recommend (but not required) that each line in this section follow the same format as the info section. That would be to store values in a key:value format, where the key is application specific and the value would be the data saved by the utility for that key.

It is also recommended (but not required) that if your utility is adding data to this section, to add it to the end of any existing lines, starting on its own new line. And your utility should preserve the order of the lines.

Be aware that some map developers use the comment section to store notes to themselves about issues with the map. This just enforces that there is no format for any data in this section and thus external utilities need to preserve any data in this section that is not part of that utility.

Example of an empty section:
```mms
comments{
}
```

Example of map developer comments: (see LRRC\frozenfrenzy.dat)
```mms
comments{
you love to see it
note: landslide timers have been doubled in the cavern, since you have two tiles to landslide onto the one tile
 which I think LRR worked on a ground-tile basis for landslides (not wall-basis)
 so this should bring the landslides slightly closer to LRR's rates
 ... maybe
}
```

Example of 3rd party utility comments: (MMMM utility)
```mms
comments{
Author:NuvaHammer
LevelType1:Panic
LevelType2:Puzzle
Length:Medium
Asset:
Info:Specialist this mission is critical. A volcano just erupted in the cavern we were using for our vehicle depot. The evacuation is in progress but we won't be able to get all the vehicles out. We sent a team of demolitionist to reroute a nearby river. Unfortunately they were a little trigger happy and now lava is flowing down the canal they made. We need you to drill out a new canal for the river before the lava reaches the vehicle depot.

You must be careful though, the canal cannot be split. So it is imperative you pick the right direction or all will be lost. 

Good Luck Cadet

Note: This level was made on early scripting features,so the lava flow is based off of time and the clock cannot be stopped. So if you win, you may still lose.
}
```
> It is very important that developers that are going to modify this section make sure they do not place a closing braces by itself as part of their data without some leading spaces. Remember - a single closing braces by itself with no leading spaces on its own line will terminate the comment section.

Example for embedded closing braces - notice that the embedded closing braces is indented with spaces:
```
comment{
    my private data that includes a closing braces
    }  
}