---
title: Packet Structure
nav-order: 2
---

# Terraria Packet Structure
All packets in the latest Terraria release.

## Basic Structure

| Size | Type | Description            |
|:-----|:-----|:-----------------------|
| 2    | U16  | Packet Length In Bytes |
| 1    | U8   | Packet ID              |
| ?    | ?    | Data                   |


## Connect Request [1]
Server {: .label }

| Size | Type   | Description     | Notes                                                        |
|:-----|:-------|:----------------|:-------------------------------------------------------------|
| ?    | String | Release Version | Formatted as so: `Terraria[ReleaseNum]`, e.g. `Terraria244`. |


## Disconnect [2]
Client {: .label }

| Size | Type   | Description       | Notes |
|:-----|:-------|:------------------|:------|
| ?    | String | Disconnect Reason | -     |


## Continue Connecting/Set User Slot [3]
Client {: .label }

| Size | Type | Description | Notes                                                                                                         |
|:-----|:-----|:------------|:--------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Player ID   | Unfortunately since the type of this is a byte, there can only be a maximum of 255 players connected at once. |


## Player Info [4]
Both {: .label }

| Size | Type   | Description      | Notes                                                                                                                                             |
|:-----|:-------|:-----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8     | Player ID        | -                                                                                                                                                 |
| 1    | U8     | Skin Variant     | -                                                                                                                                                 |
| 1    | U8     | Hair             | -                                                                                                                                                 |
| ?    | String | Player Name      | -                                                                                                                                                 |
| 1    | U8     | Hair Dye         | -                                                                                                                                                 |
| 1    | U8     | Hide Visuals     | Not sure what this does                                                                                                                           |
| 1    | U8     | Hide Visuals 2   | Not sure what this does                                                                                                                           |
| 1    | U8     | Hide Misc        | -                                                                                                                                                 |
| 3    | Color  | Hair Color       | -                                                                                                                                                 |
| 3    | Color  | Skin Color       | -                                                                                                                                                 |
| 3    | Color  | Eye Color        | -                                                                                                                                                 |
| 3    | Color  | Shirt Color      | -                                                                                                                                                 |
| 3    | Color  | Undershirt Color | -                                                                                                                                                 |
| 3    | Color  | Pants Color      | -                                                                                                                                                 |
| 3    | Color  | Shoe Color       | -                                                                                                                                                 |
| 1    | U8     | Difficulty Flags | Bits: 1: Softcore, 2: Mediumcore, 3: Hardcore, 4: Extra Accessory, 5: Creative (Journey) <br> <br> Only one of the first 3 bits should be active. |
| 3    | U8     | Torch Flags      | Bits: 1: Using Biome Torches, 2: Happy Fun Torch Time, 3: Unlocked Biome Torches.                                                                 |