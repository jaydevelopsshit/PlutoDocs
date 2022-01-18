---
title: Packet Structure
nav-order: 2
---

# Terraria Packet Structure
All packets in the latest Terraria release.

## Basic Structure
| Size | Description            | Type |
|:-----|:-----------------------|:-----|
| 2    | Packet Length In Bytes | U16  |
| 1    | Packet ID              | U8   |
| ?    | Data                   | ?    |

## Connect Request [1]
Client -> Server

| Size | Type   | Description     | Notes                                                        |
|:-----|:-------|:----------------|:-------------------------------------------------------------|
| ?    | String | Release Version | Formatted as so: `Terraria[ReleaseNum]`, e.g. `Terraria244`. |
## Disconnect [2]
Server -> Client

| Size | Type   | Description       | Notes |
|:-----|:-------|:------------------|:------|
| ?    | String | Disconnect Reason | -     |