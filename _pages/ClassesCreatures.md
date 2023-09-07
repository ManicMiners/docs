# Creature Class
The creature class is used to create a reference to a creature. With that reference you can then call on and use triggers and properties exclusive to that creature. You may also refer to a creature collection where you may use triggers connected to every building of a specific type.

## Declaration

```mms
	creature MyMonster=2
```

This declares the creature with an ID of 2 as `MyMonster`.

## Triggers

|Name|Description|
|---|---|
|dead|Trigger when a creature gets killed or enters rock.|

## Properties

|Property|Type|Note|
|---|---|---|
|row|Integer|Returns row of the creature.|
|col|Integer|Returns column of the creature.|


## Collections 
Each native creature class have their own collection. When used by itself the collection return the total amount of creatures of that type. The collection can utilize triggers but not properties.

### Making a creature flee
Use the flee: event to cause a creature to flee to that location. TODO does flee work with all types?

```mms
	flee:MyMonster,row,col;
```

### List of collections

|Name|
|---|
|CreatureRockMonster_C|
|CreatureIceMonster_C|
|CreatureLavaMonster_C|
|CreatureSlimySlug_C|
|CreatureSmallSpider_C|
|CreatureBat_C|

