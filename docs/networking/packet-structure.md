---
layout: default
title: Packet Structure
parent: Networking
nav_order: 2
---

# Packet Structure
All packets and their structure in the latest Terraria release.

## Basic Structure

| Size | Type | Description            |
|:-----|:-----|:-----------------------|
| 2    | U16  | Packet Length In Bytes |
| 1    | U8   | Packet ID              |
| ?    | ?    | Packet Data            |


## Connect Request [1]
{: .d-inline-block }

Server
{: .label }


| Size | Type   | Description    | Notes                                                        |
|:-----|:-------|:---------------|:-------------------------------------------------------------|
| ?    | String | Version        | Formatted as so: `Terraria[ReleaseNum]`, e.g. `Terraria244`. |


## Disconnect [2]
{: .d-inline-block }

Client
{: .label }


| Size | Type                                                                               | Description       | Notes |
|:-----|:-----------------------------------------------------------------------------------|:------------------|:------|
| ?    | <a href="/TerrariaDocs/docs/data-structures#network-text">Network Text</a>         | Disconnect Reason | -     |


## Continue Connecting/Set User Slot [3]
{: .d-inline-block }

Client
{: .label }


| Size | Type    | Description           | Notes                                                                                                         |
|:-----|:--------|:----------------------|:--------------------------------------------------------------------------------------------------------------|
| 1    | U8      | Player UID            | Unfortunately since the type of this is a byte, there can only be a maximum of 255 players connected at once. |
| 1    | Boolean | ServerSpecialFlags[3] | ServerWantsToRunCheckBytesInClientLoopThread                                                                  |


## Player Info [4]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type   | Description      | Notes                                                                                                                                                       |
|:-----|:-------|:-----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8     | Player UID       | -                                                                                                                                                           |
| 1    | U8     | Skin Variant     | -                                                                                                                                                           |
| 1    | U8     | Hair             | -                                                                                                                                                           |
| ?    | String | Player Name      | -                                                                                                                                                           |
| 1    | U8     | Hair Dye         | -                                                                                                                                                           |
| 1    | U8     | Hide Visuals     | -                                                                                                                                                           |
| 1    | U8     | Hide Visuals 2   | -                                                                                                                                                           |
| 1    | U8     | Hide Misc        | -                                                                                                                                                           |
| 3    | Color  | Hair Color       | -                                                                                                                                                           |
| 3    | Color  | Skin Color       | -                                                                                                                                                           |
| 3    | Color  | Eye Color        | -                                                                                                                                                           |
| 3    | Color  | Shirt Color      | -                                                                                                                                                           |
| 3    | Color  | Undershirt Color | -                                                                                                                                                           |
| 3    | Color  | Pants Color      | -                                                                                                                                                           |
| 3    | Color  | Shoe Color       | -                                                                                                                                                           |
| 1    | U8     | Difficulty Flags | Bits: 1: Softcore, 2: Mediumcore, 3: Hardcore, 4: Extra Accessory, 5: Creative (Journey). <br> <br> Only one of the first 3 bits should be active.          |
| 1    | U8     | Flags 2          | Bits: 1: Using Biome Torches, 2: Happy Fun Torch Time, 3: Unlocked Biome Torches, 4: Unlocked Super Cart, 5: Enabled Super Cart.                            |
| 1    | U8     | Flags 3          | Bits: 1: Used Aegis Crystal, 2: Used Aegis Fruit, 3: Used Arcane Crystal, 4: Used Galaxy Pearl, 5: Used Gummy Worm, 6: Used Ambrosia, 7: Ate Artisan Bread. |


## Set Player Inventory Slot [5]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes                                      |
|:-----|:-----|:------------|:-------------------------------------------|
| 1    | U8   | Player UID  | -                                          |
| 2    | S16  | Slot Index  | -                                          |
| 2    | S16  | Stack Size  | This should never be below 1 or above 999. |
| 1    | U8   | Item Prefix | -                                          |
| 2    | S16  | Item Net ID | -                                          |


## Request World Info [6]
{: .d-inline-block }

Server
{: .label }
Requests that <a href="#world-info-7">World Info</a> be sent.

**No Data**


## World Info [7]
{: .d-inline-block }

Client
{: .label }
Sends a lot of information about the world and its current state.

| Size | Type            | Description                 | Notes                                                                                                                                                         |
|:-----|:----------------|:----------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 4    | S32             | Time                        | -                                                                                                                                                             |
| 1    | U8              | Day and Moon Flags          | Bits: 1: Day Time, 2: Blood Moon, 3: Eclipse.                                                                                                                 |
| 1    | U8              | Moon Phase                  | -                                                                                                                                                             |
| 2    | S16             | Max Tiles X (World Width)   | -                                                                                                                                                             |
| 2    | S16             | Max Tiles Y (World Height)  | -                                                                                                                                                             |
| 2    | S16             | Spawn X                     | -                                                                                                                                                             |
| 2    | S16             | Spawn Y                     | -                                                                                                                                                             |
| 2    | S16             | Surface layer               | Y Coordinate of the world's surface layer.                                                                                                                    |
| 2    | S16             | Rock Layer                  | Y Coordinate of the world's rock layer.                                                                                                                       |
| 4    | S32             | World ID                    | -                                                                                                                                                             |
| ?    | String          | World Name                  | -                                                                                                                                                             |
| 1    | U8              | Difficulty                  | 1: Normal, 2: Expert, 3: Master, 4: Creative (Journey).                                                                                                       |
| 1    | UUID (U8 Array) | World UUID                  | -                                                                                                                                                             |
| 1    | U64             | World Generator Version     | -                                                                                                                                                             |
| 1    | U8              | Moon Type                   | -                                                                                                                                                             |
| 1    | U8              | Tree Background 1           | -                                                                                                                                                             |
| 1    | U8              | Corruption Background       | -                                                                                                                                                             |
| 1    | U8              | Jungle Background           | -                                                                                                                                                             |
| 1    | U8              | Snow Background             | -                                                                                                                                                             |
| 1    | U8              | Hallow Background           | -                                                                                                                                                             |
| 1    | U8              | Crimson Background          | -                                                                                                                                                             |
| 1    | U8              | Desert Background           | -                                                                                                                                                             |
| 1    | U8              | Ocean Background            | -                                                                                                                                                             |
| 1    | U8              | Mushroom Background         | -                                                                                                                                                             |
| 1    | U8              | Underworld Background       | -                                                                                                                                                             |
| 1    | U8              | Tree Background 2           | -                                                                                                                                                             |
| 1    | U8              | Tree Background 3           | -                                                                                                                                                             |
| 1    | U8              | Tree Background 4           | -                                                                                                                                                             |
| 1    | U8              | Ice Back Style              | -                                                                                                                                                             |
| 1    | U8              | Jungle Back Style           | -                                                                                                                                                             |
| 1    | U8              | Hell Back Style             | -                                                                                                                                                             |
| 4    | Float           | Wind Speed Target           | -                                                                                                                                                             |
| 1    | U8              | Cloud Count                 | -                                                                                                                                                             |
| 4    | S32             | Tree X 1                    | -                                                                                                                                                             |
| 4    | S32             | Tree X 2                    | -                                                                                                                                                             |
| 4    | S32             | Tree X 3                    | -                                                                                                                                                             |
| 1    | U8              | Tree Style 1                | -                                                                                                                                                             |
| 1    | U8              | Tree Style 2                | -                                                                                                                                                             |
| 1    | U8              | Tree Style 3                | -                                                                                                                                                             |
| 1    | U8              | Tree Style 4                | -                                                                                                                                                             |
| 4    | S32             | Cave Back X 1               | -                                                                                                                                                             |
| 4    | S32             | Cave Back X 2               | -                                                                                                                                                             |
| 4    | S32             | Cave Back X 3               | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 1           | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 2           | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 3           | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 4           | -                                                                                                                                                             |
| 1    | U8              | Forest 1 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Forest 2 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Forest 3 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Forest 4 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Corruption Tree Top Style   | -                                                                                                                                                             |
| 1    | U8              | Jungle Tree Top Style       | -                                                                                                                                                             |
| 1    | U8              | Snow Tree Top Style         | -                                                                                                                                                             |
| 1    | U8              | Hallow Tree Top Style       | -                                                                                                                                                             |
| 1    | U8              | Crimson Tree Top Style      | -                                                                                                                                                             |
| 1    | U8              | Desert Tree Top Style       | -                                                                                                                                                             |
| 1    | U8              | Ocean Tree Top Style        | -                                                                                                                                                             |
| 1    | U8              | Mushroom Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Underworld Tree Top Style   | -                                                                                                                                                             |
| 4    | Float           | Max Rain                    | -                                                                                                                                                             |
| 1    | U8              | Event Info 1                | Bits: 1: Shadow Orb Smashed, 2: Downed Boss 1, 3: Downed Boss 2, 4: Downed Boss 3, 5: Hardmode, 6: Downed Clown, 7: Server Side Character, 8: Downed Plantera |
| 1    | U8              | Event Info 2                | -                                                                                                                                                             |
| 1    | U8              | Event Info 3                | -                                                                                                                                                             |
| 1    | U8              | Event Info 4                | -                                                                                                                                                             |
| 1    | U8              | Event Info 5                | -                                                                                                                                                             |
| 1    | U8              | Event Info 6                | -                                                                                                                                                             |
| 1    | U8              | Event Info 7                | -                                                                                                                                                             |
| 1    | U8              | Event Info 8                | -                                                                                                                                                             |
| 1    | U8              | Event Info 9                | -                                                                                                                                                             |
| 1    | U8              | Event Info 10               | -                                                                                                                                                             |
| 1    | U8              | Sundial Cooldown            | -                                                                                                                                                             |
| 1    | U8              | Moondial Cooldown           | -                                                                                                                                                             |
| 2    | S16             | Copper/Tin Ore Tier         | Block ID 7 (Copper) or 166 (Tin).                                                                                                                             |
| 2    | S16             | Iron/Lead Ore Tier          | Block ID 6 (Iron) or 167 (Lead).                                                                                                                              |
| 2    | S16             | Silver/Tungsten Ore Tier    | Block ID 9 (Silver) 168 (Tungsten).                                                                                                                           |
| 2    | S16             | Gold/Platinum Ore Tier      | Block ID 8 (Gold) or 169 (Platinum).                                                                                                                          |
| 2    | S16             | Cobalt/Palladium Ore Tier   | Block ID 107 (Cobalt) or 221 (Palladium).                                                                                                                     |
| 2    | S16             | Mythril/Orichalcum Ore Tier | Block ID 108 (Mythril) or 222 (Orichalcum).                                                                                                                   |
| 2    | S16             | Adamantite/Titanium         | Block ID 111 (Adamantite) or 223 (Titanium).                                                                                                                  |
| 1    | S8              | Invasion Type               | -                                                                                                                                                             |
| 8    | U64             | Lobby ID                    | Always 0, except if using the Steam Social API.                                                                                                               |
| 4    | Float           | Sandstorm Severity          | -                                                                                                                                                             |


## Request Spawn Tiles [8]
{: .d-inline-block }

Server
{: .label }

| Size | Type | Description    | Notes |
|:-----|:-----|:---------------|:------|
| 4    | S32  | Player Spawn X | -     |
| 4    | S32  | Player Spawn Y | -     |


## Status [9]
{: .d-inline-block }

Client
{: .label }

| Size | Type                                                                               | Description   | Notes                                             |
|:-----|:-----------------------------------------------------------------------------------|:--------------|:--------------------------------------------------|
| 4    | S32                                                                                | Max           | Only increments.                                  |
| ?    | <a href="/TerrariaDocs/docs/data-structures#network-text">Network Text</a>         | Text          | -                                                 |
| 1    | U8                                                                                 | Flags         | Bits: 1: Hide Status Percent, 2: Text Shadowed.   |


## Send Tile Section [10]
{: .d-inline-block }

Client
{: .label }

| Size | Type    | Description       | Notes                                                                                 |
|:-----|:--------|:------------------|:--------------------------------------------------------------------------------------|
| 1    | Boolean | Compressed        | If true, the rest of the data written should be compressed via the deflate algorithm. |
| 4    | S32     | Start X           | -                                                                                     |
| 4    | S32     | Start Y           | -                                                                                     |
| 2    | S16     | Width             | -                                                                                     |
| 2    | S16     | Height            | -                                                                                     |
| ?    | -       | Tiles             | -                                                                                     |
| 2    | S16     | Chest Count       | -                                                                                     |
| ?    | -       | Chests            | -                                                                                     |
| 2    | S16     | Sign Count        | -                                                                                     |
| ?    | -       | Signs             | -                                                                                     |
| 2    | S16     | Tile Entity Count | -                                                                                     |
| ?    | -       | Tile Entities     | -                                                                                     |


## Tile Section Frame [11] (Deprecated)
{: .d-inline-block }

Client
{: .label }

| Size | Type | Description     | Notes |
|:-----|:-----|:----------------|:------|
| 2    | S16  | Start Section X | -     |
| 2    | S16  | Start Section Y | -     |
| 2    | S16  | End Section X   | -     |
| 2    | S16  | End Section Y   | -     |


## Spawn Player [12]
{: .d-inline-block }

Server
{: .label }

| Size | Type | Description            | Notes                                                               |
|:-----|:-----|:-----------------------|:--------------------------------------------------------------------|
| 1    | U8   | Player UID             | -                                                                   |
| 2    | S16  | Spawn X                | -                                                                   |
| 2    | S16  | Spawn Y                | -                                                                   |
| 2    | S16  | Number of Deaths PVE   | -                                                                   |
| 2    | S16  | Number of Deaths PVP   | -                                                                   |
| 4    | S32  | Respawn Time Remaining | If this is more than 0, then the player is still dead.              |
| 1    | U8   | Context                | 0: Revived From Death, 1: Spawning Into World, 2: Recall From Item. |


## Update Player [13]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type  | Description         | Notes                                                                                                                                                                 |
|:-----|:------|:--------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8    | Player UID          | -                                                                                                                                                                     |
| 1    | U8    | Control Flags       | Bits: 1: Up, 2: Down, 3: Left, 4: Right, 5: Jump, 6: Use Item, 7: Direction;                                                                                          |
| 1    | U8    | Pulley Flags        | Bits: 1: Pulley Enabled, 2: Direction, 3: Update Velocity, 4: Vortex Stealth Active, 5: Gravity Direction, 6: Shield Raised.                                          |
| 1    | U8    | Misc Flags          | Bits: 1: Hovering Up, 2: Void Vault Enabled, 3: Sitting, 4: Downed DD2 Event, 5: Petting Animal, 6: Petting Small Animal, 7: Used Potion of Return, 8: Hovering Down. |
| 1    | U8    | Sleeping Flags      | Bits: 1: Sleeping.                                                                                                                                                    |
| 1    | U8    | Selected Item       | Probably an inventory ID.                                                                                                                                             |
| 4    | Float | Position X          | -                                                                                                                                                                     |
| 4    | Float | Position Y          | -                                                                                                                                                                     |
| 4    | Float | Velocity X          | Only sent if the `Update Velocity` bit in `Pulley Flags` is active.                                                                                                   |
| 4    | Float | Velocity Y          | Only sent if the `Update Velocity` bit in `Pulley Flags` is active.                                                                                                   |
| 4    | Float | Original Position X | Original Position X for Potion of Return, only sent if the `Used Potion of Return` bit in `Misc Flags` is active.                                                     |
| 4    | Float | Original Position Y | Original Position Y for Potion of Return, only sent if the `Used Potion of Return` bit in `Misc Flags` is active.                                                     |
| 4    | Float | Home Position X     | Home Position X for Potion of Return, only sent if the `Used Potion of Return` bit in `Misc Flags` active.                                                            |
| 4    | Float | Home Position Y     | Home Position Y for Potion of Return, only sent if the `Used Potion of Return` bit in `Misc Flags` is active.                                                         |


## Player Active [14]
{: .d-inline-block }

Client
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 1    | U8   | Player UID  | -     |
| 1    | U8   | Active      | -     |


## Null [15]
{: .d-inline-block }

Never Sent
{: .label .label-red }

**No Data**


## Player HP [16]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes                                     |
|:-----|:-----|:------------|:------------------------------------------|
| 1    | U8   | Player UID  | -                                         |
| 2    | S16  | HP          | This should never be under 0 or over 600. |
| 2    | S16  | Max HP      | This should never be under 0 or over 600. |


## Modify Tile [17]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:-----|:-----|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Action      | 0: Remove Block, 1: Place Block, 2: Remove Wall, 3: Place Wall, 4: Remove Tile No Item, 5: Place Red Wire, 6: Remove Red Wire, 7: Pound Block, 8: Place Actuator, 9: Remove Actuator, 10: Place Blue Wire, 11: Remove Blue Wire, 12: Place Green Wire, 13: Remove Green Wire, 14: Slope Block, 15: Frame Track, 16: Place Yellow Wire, 17: Remove Yellow Wire, 18: Poke Logic Gate, 19: Actuate, 20: Remove Block (?), 21: Replace Block, 22: Replace Wall, 23: Slope Pound Block. |
| 2    | S16  | Tile X      | -                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 2    | S16  | Tile Y      | -                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 2    | S16  | Data        | Provides necessary data for the action in this packet if it's needed. <br><br> Remove Block: (Boolean)Failed, Place Block: (S16)Block ID, Remove Wall: (Boolean)Failed, Place Wall: (S16)Wall ID, Remove Tile No Item: (Boolean)Failed, Slope Block: (S16)Slope, Replace Block: (S16)Block ID, Replace Wall: (S16)Wall ID.                                                                                                                                                         |
| 1    | U8   | Extra Data  | Provides extra data for the action in this packet if it's needed. <br><br> Place Tile: (U8)Style, Replace Tile: (U8)Style                                                                                                                                                                                                                                                                                                                                                          |


## Time [18]
{: .d-inline-block }

Client
{: .label }

| Size | Type    | Description | Notes |
|:-----|:--------|:------------|:------|
| 1    | Boolean | Day Time    | -     |
| 4    | S32     | Time        | -     |
| 2    | S16     | Sun Mod X   | -     |
| 2    | S16     | Sun Mod Y   | -     |


## Door Toggle [19]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes                                                                                                                                                                                                                                      |
|:-----|:-----|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Action      | 0: Open Door, 1: Close Door, 2: Open Trapdoor, 3: Close Trapdoor, 4: Open Tall Gate, 5: Close Tall Gate.                                                                                                                                   |
| 2    | S16  | Tile X      | -                                                                                                                                                                                                                                          |
| 2    | S16  | Tile Y      | -                                                                                                                                                                                                                                          |
| 1    | U8   | Direction   | If the `Action` relates to trapdoors, a value of 1 means the player is above the trapdoor. Otherwise, if the `Action` is `Open Door` then a value of -1 means the door should open to the left, 1 means the door should open to the right. |


## Send Tile Square [20]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description      | Notes                           |
|:-----|:-----|:-----------------|:--------------------------------|
| 2    | U16  | Size             | -                               |
| 1    | U8   | Tile Change Type | Only if `(Size & 0x8000) != 0`. |
| 2    | S16  | Tile X           | -                               |
| 2    | S16  | Tile Y           | -                               |
| ?    | -    | Tiles            | -                               |


## Update Item Drop [21]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type  | Description | Notes                                                     |
|:-----|:------|:------------|:----------------------------------------------------------|
| 2    | S16   | Item UID    | If this is below 400 and `Item ID` is 0 then this is air. |
| 4    | Float | Position X  | -                                                         |
| 4    | Float | Position Y  | -                                                         |
| 4    | Float | Velocity X  | -                                                         |
| 4    | Float | Velocity Y  | -                                                         |
| 2    | S16   | Stack Size  | This should never be below 1 or above 999.                |
| 1    | U8    | Item Prefix | -                                                         |
| 1    | U8    | No Delay    | -                                                         |
| 2    | S16   | Item Net ID | -                                                         |


## Update Item Owner [22]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | Item UID    | -     |
| 1    | U8   | Player UID  | -     |


## Entity Update [23]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size  | Type       | Description         | Notes                                                                                                                               |
|:------|:-----------|:--------------------|:------------------------------------------------------------------------------------------------------------------------------------|
| 2     | S16        | Entity UID          | -                                                                                                                                   |
| 4     | Float      | Position X          | -                                                                                                                                   |
| 4     | Float      | Position Y          | -                                                                                                                                   |
| 4     | Float      | Velocity X          | -                                                                                                                                   |
| 4     | Float      | Velocity Y          | -                                                                                                                                   |
| 2     | U16        | Target              | This a player UID.                                                                                                                  |
| 1     | U8         | Entity Flags 1      | Bits: 1: Direction, 2: Direction Y, 3: Entity AI 1, 4: Entity AI 2, 5: Entity AI 3, 6: Entity AI 4, 7: Sprite Direction, 8: Max HP. |
| 1     | U8         | Entity Flags 2      | Bits: 1: Stats Scaled, 2: Spawned From Statue, 3: Strength Multiplier.                                                              |
| 4     | Float      | Entity AI 1         | Only sent if the `Entity AI 1` flag in `Entity Flags 1` is active.                                                                  |
| 4     | Float      | Entity AI 2         | Only sent if the `Entity AI 2` flag in `Entity Flags 1` is active.                                                                  |
| 4     | Float      | Entity AI 3         | Only sent if the `Entity AI 3` flag in `Entity Flags 1` is active.                                                                  |
| 4     | Float      | Entity AI 4         | Only sent if the `Entity AI 4` flag in `Entity Flags 1` is active.                                                                  |
| 2     | S16        | Entity Net ID       | -                                                                                                                                   |
| 1     | U8         | Player Count        | Used to scale the entity's stats if the difficulty is expert or master. Only sent if the `Stats Scaled` flag in `Entity Flags 2`.   |
| 4     | Float      | Strength Multiplier | Only sent if the `Strength Multiplier` flag in `Entity Flags 2` is active.                                                          |
| 1     | U8         | HP Bytes            | Size of `HP` in bytes. Only sent if the `Max HP` flag in `Entity Flags 1` is inactive.                                              |
| 1/2/4 | S8/S16/S32 | HP                  | Either a S8, S16, or S32 according to `HP Bytes`. Only sent if the `Max HP` flag in `Entity Flags 1` is inactive.                   |
| 1     | U8         | Release Owner       | This is a player UID. Only sent if this entity is catchable (fishing).                                                              |


## Strike Entity with Held Item [24]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | Entity UID  | -     |
| 1    | U8   | Player UID  | -     |


## Null [25]
{: .d-inline-block }

Never Sent
{: .label .label-red }

**No Data**


## Null [26]
{: .d-inline-block }

Never Sent
{: .label .label-red }

**No Data**


## Projectile Update [27]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type  | Description     | Notes                                                                                                                   |
|:-----|:------|:----------------|:------------------------------------------------------------------------------------------------------------------------|
| 2    | S16   | Projectile UID  | -                                                                                                                       |
| 4    | Float | Position X      | -                                                                                                                       |
| 4    | Float | Position Y      | -                                                                                                                       |
| 4    | Float | Velocity X      | -                                                                                                                       |
| 4    | Float | Position Y      | -                                                                                                                       |
| 1    | U8    | Owner           | This is a player UID.                                                                                                   |
| 2    | S16   | Projectile ID   | -                                                                                                                       |
| 1    | U8    | Flags           | Bits: 1: AI 1, 2: AI 2, 3: Damage, 4: Knockback, 5: Original Damage, 6: UUID.                                           |
| 4    | Float | AI 1            | Only sent if the `AI 1` flag in `Flags` is active.                                                                      |
| 4    | Float | AI 2            | Only sent if the `AI 2` flag in `Flags` is active.                                                                      |
| 2    | S16   | Damage          | Only sent if the `Damage` flag in `Flags` is active.                                                                    |
| 4    | Float | Knockback       | Only sent if the `Knockback` flag in `Flags` is active.                                                                 |
| 2    | S16   | Original Damage | Only sent if the `Original Damage` flag in `Flags` is active.                                                           |
| 2    | S16   | Projectile UUID | This is not actually a Universally Unique Identifier, rather an S16. Only sent if the `UUID` flag in `Flags` is active. |


## Entity Strike [28]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type    | Description   | Notes |
|:-----|:--------|:--------------|:------|
| 2    | S16     | Entity UID    | -     |
| 1    | S16     | Damage        | -     |
| 4    | Float   | Knockback     | -     |
| 1    | U8      | Hit Direction | -     |
| 1    | Boolean | Critical      | -     |


## Destroy Projectile [29]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description    | Notes                 |
|:-----|:-----|:---------------|:----------------------|
| 2    | S16  | Projectile UID | -                     |
| 1    | U8   | Owner          | This is a player UID. |


## Toggle PVP [30]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type    | Description | Notes |
|:-----|:--------|:------------|:------|
| 1    | S16     | Player UID  | -     |
| 1    | Boolean | PVP Enabled | -     |


## Open Chest [31]
{: .d-inline-block }

Server
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | Tile X      | -     |
| 2    | S16  | Tile Y      | -     |


## Update Chest Item [32]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | Chest UID   | -     |
| 1    | U8   | Item Slot   | -     |
| 2    | S16  | Stack Size  | -     |
| 1    | U8   | Prefix ID   | -     |
| 2    | S16  | Item Net ID | -     |


## Sync Active Chest [33]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type       | Description | Notes                            |
|:-----|:-----------|:------------|:---------------------------------|
| 2    | S16        | Chest UID   | -                                |
| 2    | S16        | Chest X     | -                                |
| 2    | S16        | Chest Y     | -                                |
| 1    | U8         | Name Length | This should be between 0 and 20. |
| ?    | Raw String | Name        | Read based off `Name Length`.    |


## Place Chest [34]
{: .d-inline-block }

Both
{: .label }

| Size | Type | Description         | Notes                                                                                                               |
|:-----|:-----|:--------------------|:--------------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Action              | Bits: 1: Place Chest, 2: Kill Chest, 3: Place Dresser, 4: Kill Dresser, 5: Place Containers 2, 6: Kill Container 2. |
| 2    | S16  | Tile X              | -                                                                                                                   |
| 2    | S16  | Tile Y              | -                                                                                                                   |
| 2    | S16  | Style               | -                                                                                                                   |
| 2    | S16  | Chest ID to destroy | ID if client is receiving packet, otherwise 0.                                                                      |


## Heal Effect [35]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 1    | U8   | Player UID  | -     |
| 2    | S16  | Heal Amount | -     |


## Player Zone [36]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description  | Notes                                                                                                                                                  |
|:-----|:-----|:-------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Player UID   | -                                                                                                                                                      |
| 1    | U8   | Zone Flags 1 | Bits: 1: Dungeon, 2: Corruption, 3: Holy, 4: Meteor, 5: Jungle, 6: Snow, 7: Crimson, 8: Water Candle.                                                  |
| 1    | U8   | Zone Flags 2 | Bits: 1: Peace Candle, 2: Solar Pillar, 3: Vortex Pillar, 4: Nebula Pillar, 5: Stardust Pillar, 6: Desert, 7: Glowing Mushroom, 8: Underground Desert. |


## Password Required [37]
{: .d-inline-block }

Server
{: .label }

**No Data**


## Password Send [38]
{: .d-inline-block }

Client
{: .label }

| Size | Type   | Description | Notes |
|:-----|:-------|:------------|:------|
| ?    | String | Password    | -     | 


## Remove Item Owner [39]
{: .d-inline-block }

Server
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | Item Index  | -     |


## Set Active NPC [40]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type  | Description    | Notes |
|:-----|:------|:---------------|:------|
| 8    | U8    | Player UID     | -     |
| 4    | Float | Item Rotation  | -     |
| 2    | S16   | Item Animation | -     |


## Player Item Animation [41]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type  | Description    | Notes |
|:-----|:------|:---------------|:------|
| 1    | U8    | Player UID     | -     |
| 4    | Float | Item Rotation  | -     |
| 2    | S16   | Item Animation | -     |


## Player Mana [42]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 1    | U8   | Player UID  | -     |
| 2    | S16  | Mana        | -     |
| 2    | S16  | Max Mana    | -     | 


## Mana Effect [43]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 1    | U8   | Player UID  | -     |
| 2    | S16  | Mana Amount | -     |


## Null [44]
{: .d-inline-block }

Never Sent
{: .label .label-red }

**No Data**


## Player Team [45]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 1    | U8   | Player UID  | -     |
| 1    | U8   | Team        | -     |


## Request Sign [46]
{: .d-inline-block }

Client
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | X           | -     |
| 2    | S16  | Y           | -     |


## Update Sign [47]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type   | Description | Notes |
|:-----|:-------|:------------|:------|
| 2    | S16    | Sign UID    | -     |
| 2    | S16    | X           | -     |
| 2    | S16    | Y           | -     |
| ?    | String | Text        | -     |
| 1    | U8     | Player UID  | -     |
| 1    | U8     | Sign Flags  | TODO  |


## Set Liquid [48]
{: .d-inline-block }

Both (Sync)
{: .label }

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 2    | S16  | X           | -     |
| 2    | S16  | Y           | -     |
| 1    | U8   | Liquid      | -     |
| 1    | U8   | Liquid Type | -     |


## Complete Connection And Spawn [49]
{: .d-inline-block }

Server
{: .label }

**No Data**

## Player Buffs [50]
{: .d-inline-block }

Both
{: .label }

| Size | Type    | Description  | Notes |
|:-----|:--------|:-------------|:------|
| 1    | U8      | Player UID   | -     |
| 88   | U16[44] | Player Buffs | -     |