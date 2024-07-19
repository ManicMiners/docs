# DAT Section comments

The comment section is a section that is not modified by the map editor. It is for any purpose and there is no specification on how it is intended to be used.

The map editor will read each line in this section and write out those lines when the map is saved without any modification. When a new map is created, this section is empty.

In general this section is for use by external DAT utilities.

While there is no specification on how this section is to be formatted, it is generally understood that external utilities would look in this section for data they have written before and ignore any data that was not part of that utility.

To easily support any external utility, it is recommend (but not required) that each line in this section follow the same format as the info section. That would be to store values in a key:value format, where the key is application specific and the value would be the data saved by the utility for that key.

It is also recommended (but not required) that if your utility is adding data to this section, to add it to the end of any existing lines, starting on its own new line. And your utility should preserve the order of the lines.

Be aware that some map developers use the comment section to store notes to themselves about issues with the map. This just enforces that there is no format for any data in this section and thus external utilities need to preserve any data in this section that is not part of that utility.


