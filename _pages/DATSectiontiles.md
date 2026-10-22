# DAT Section tiles
The tiles section is required and written by the map editor on every save. It contains the TileID of every tile in the map.

0,0 is the upper left tile, and rows-1,cols-1 is the lower right tile.

The section has one line of column values (starting at column 0) for each row in the map.

Each line contains a `TileID,` for that column tile. After all columns are written a new line is started.  Every value is followed by a comma. There are no spaces.

TileIDs are between 1 and 175. Any values outside of this range are invalid.

There must be exactly `rowcount` (from the info section) rows in the tiles section.
There must be exactly `colcount` (from the info section) columns in each row.

Generally the border tiles - the ones around the edge of the map - are solid rock regular (id: 38).

TileIDs may have a +100 value added to them - these are ground tiles that are part of an undiscovered cavern.

TileIDs may have a +50 value added to them - these are walls that have been reinforced. 

Example of a 3x3 map. The border is solid rock regular; the single floor tile is ground.


```mms
tiles{
38,38,38,
38,1,38,
38,38,38,
}
```


[List of TileIDs](_pages/DATTileReference)