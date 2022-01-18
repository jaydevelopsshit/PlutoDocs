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