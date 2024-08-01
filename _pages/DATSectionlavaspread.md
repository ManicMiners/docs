# DAT Section lavaspread

The lavaspread section lists all of the tiles that have lava erosion assigned to them. Erosion tiles have two values, first is the interval between the phases of erosion and the second is the initial delay before erosion begins.  The editor organizes the list into groups that have the same interval and delay, and outputs all of them on the same line.

Format:

```
INTERVAL/DELAY:ROW,COL/ROW,COL/...
```

## INTERVAL

The interval is a floating point number representing the number of seconds between each phase of erosion. This is a minimum number of seconds, the game engine uses a random value between this value and 2x the value. The editor outputs values to the 0.1 resolution, it may be that internally erosions are collected into groups at the 0.1 second interval.

## DELAY
Delay is a floating point number representing the number of seconds to delay before starting the erosion processes. This value is output rounded to the 0.1 resolution.

## ROW,COL/

Each tile that has an erosion at that interval and delay is listed, row,column order followed by a forward slash.  There does not appear to be a limit (up to the size of the map) on the number of tiles that may have the same interval.

>It is invalid to list the same tile having multiple erosion intervals, thus every tile may only be listed a single time.

>The engine requires that all tiles having erosion with the same interval and delay MUST be listed together on the same line. Additional lines with the same interval and delay are ignored.

## Example

Within a map, there are three groups of erosion cool downs:
- 30.0 seconds with 10.0 second delay has a single tile.
- 15.0 seconds with 10.0 second delay has two tiles.
- 7.0 seconds with 10.0 second delay has three tiles

```
lavaspread{
30.0/10.0:1,1/
15.0/10.0:1,2/1,3/
7.0/10.0:1,4/1,5/1,6/
}
```

## General Information

There is no known way to create a new automatic erosion from script. There is no known macro that returns the number of active erosions (unlike landslides). However with advanced scripting logic one could simulate lava spreading or even the processes of erosion as part of the spread. This would be done by changing a tiles value over time.

Erosions that are in undiscovered caverns are not active until discovered.

Erosions require a neighboring tile be lava. After the delay, the tile will progress through the five erosions phases.

1. Erosion 1 (TileID 10)
2. Erosion 2 (TileID 9)
3. Erosion 3 (TileID 8)
4. Erosion 4 (TileID 7)
5. Lava. (TileID 6)

If a tile starts at an erosion phase, after the delay and interval it will progresses starting at the next phase. 

## erosionscale

info section erosionscale value is used to initially set the script erosionscale macro. This value multiplies the interval of erosion. By default 1.0 has no effect. A value of 2.0 will double the erosion interval time.  Setting erosionscale to 0.0 will permanently disable erosion in the map.

## erosioninitialwaittime

info section erosioninitialwaittime is used to globally delay all erosions for the given number of seconds from the loading of the map. After this delay, erosions continue normally. Default value is 0.0 seconds.
