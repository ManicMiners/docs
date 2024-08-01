# DAT Section landslidefrequency

The landslidefrequeency section lists all of the tiles that have landslides assigned to them.  The editor sorts the list into groups that have the same interval and outputs all of them on the same line.

Format:

```
INTERVAL:ROW,COL/ROW,COL/...
```

## INTERVAL

The interval is a floating point number representing the number of seconds between each landslide. This value is the minimum number of seconds, the game engine picks a random value between this number and double the number. The editor outputs values to the 0.1 resolution, it may be that internally landslides are collected into groups at the 0.1 second interval.

## ROW,COL/

Each tile that has a landslide at that interval is listed, row,column order followed by a forward slash.  There does not appear to be a limit (up to the size of the map) on the number of tiles that may have the same interval.

>It is invalid to list the same tile having multiple landslides intervals, thus every tile may only be listed a single time.

>The engine requires that all tiles having landslides with the same interval MUST be listed together on the same line. Additional lines with the same interval are ignored.

## Example

Within a map, there are three groups of landslide cooldowns:
- 30.0 seconds has a single tile.
- 15.0 seconds has two tiles.
- 7.0 seconds has three tiles

```
landslidefrequency{
30.0:1,1/
15.0:1,2/1,3/
7.0:1,4/1,5/1,6/
}
```

## Info

There is no known way to create a new landslide from script.

`EventLandslide_C` is a collection macro that returns the number of active landslides as an int.

Landslides that are in undiscovered caverns are not active until discovered.

For a landslide to be active, it must be one of the following wall types (it cannot be a wall corner tile) and it must fall into a floor tile that is not water or lava.
- Dirt Regular (26)
- Loose Rock Regular (30)
- Hard Rock Regular (34)

Landslides create rubble that does not contain ore. However landslides falling onto a power path do not destroy the power path.

Landslides damage miners, some vehicles, and buildings. The following vehicles are immune to landslide damage:
- VehicleCargoCarrier_C is water vehicle and there are no landslides over water.
- VehicleLoaderDozer_C is immune to landslide damage.
- VehicleRapidRider_C is a water vehicle and there are no landslides over water.
- VehicleTunnelScout_C is ariel vehicle so it moves above the landslide.
- VehicleTunnelTransport_C is aerial vehicle so it moves above the landslide.
