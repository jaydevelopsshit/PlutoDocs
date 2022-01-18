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


Server {: .label }
## Connect Request [1]

| Size | Type   | Description     | Notes                                                        |
|:-----|:-------|:----------------|:-------------------------------------------------------------|
| ?    | String | Release Version | Formatted as so: `Terraria[ReleaseNum]`, e.g. `Terraria244`. |


Client {: .label }
## Disconnect [2]

| Size | Type   | Description       | Notes |
|:-----|:-------|:------------------|:------|
| ?    | String | Disconnect Reason | -     |


Client {: .label }
## Continue Connecting/Set User Slot [3]

| Size | Type | Description | Notes                                                                                                         |
|:-----|:-----|:------------|:--------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Player ID   | Unfortunately since the type of this is a byte, there can only be a maximum of 255 players connected at once. |