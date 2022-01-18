---
layout: default
title: Terraria Data Structures
nav_order: 3
---

# Data Structures
Commonly used data structures in Terraria. The tables are their structure when they are serialized for writing.

## Color
Represents an RGB color.
<br> <br>
Examples: Character selection colors like hair color, shirt color, shoe color, etc.

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
| 1    | U8   | Red         |       | 
| 1    | U8   | Green       |       |
| 1    | U8   | Blue        |       |

## Network Text
Represents text sent over the network. It can be either literal (raw text), formattable, or a localization key (translatable).
<br> <br>
Example: <a href="/PlutoDocs/docs/networking/packet-structure#disconnect-2">Disconnect Packet</a>'s reason.

| Size | Type              | Description          | Notes                                                            |
|:-----|:------------------|:---------------------|:-----------------------------------------------------------------|
| 1    | U8                | Type                 | 0: Literal, 1: Formattable, 2: Localization Key.                 |
| ?    | String            | Text                 | If mode is translatable, then this should be a localization key. |
| 1    | U8                | Substitutions Length | Only used if mode is not set as literal.                         |
| ?    | NetworkText Array | Subsitutions         | Only used if mode is not set as literal.                         |