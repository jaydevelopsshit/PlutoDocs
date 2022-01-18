---
title: Packet Structure
nav-order: 2
---

# Terraria Packet Structure
All packets in the latest Terraria release.

## Basic Structure
<div>
| Size | Type | Description            |
|:-----|:-----|:-----------------------|
| 2    | U16  | Packet Length In Bytes |
| 1    | U8   | Packet ID              |
| ?    | ?    | Data                   |
</div>

## Connect Request [1]
Client -> Server
<div>
| Size | Type   | Description     | Notes                                                        |
|:-----|:-------|:----------------|:-------------------------------------------------------------|
| ?    | String | Release Version | Formatted as so: `Terraria[ReleaseNum]`, e.g. `Terraria244`. |
</div>
## Disconnect [2]
Server -> Client

<div>
| Size | Type   | Description       | Notes |
|:-----|:-------|:------------------|:------|
| ?    | String | Disconnect Reason | -     |
</div>