---
layout: default
title: Login Sequence
parent: Networking
nav_order: 1
---

# Login Sequence
This is an example of a normal vanilla login sequence.
<br>
1. Client connects to server
2. C -> S: <a href="/TerrariaDocs/docs/networking/packet-structure#connect-request-1">Connect Request</a>
3. S -> C: Password Required (Optional)
4. C -> S: Password Send (Optional)
5. S -> C: <a href="/TerrariaDocs/docs/networking/packet-structure#continue-connectingset-user-slot-3">Continue Connecting</a>
6. C -> S: <a href="/TerrariaDocs/docs/networking/packet-structure#player-info-4">Player Info</a>
7. C -> S: Client UUID
8. C -> S: Player HP
9. C -> S: Mana Effect
10. C -> S: Update Player Buffs
11. C -> S: Send Inventory (<a href="/TerrariaDocs/docs/networking/packet-structure#set-player-inventory-slot-5">Set Player Inventory Slot</a>)
12. C -> S: <a href="/TerrariaDocs/docs/networking/packet-structure#request-world-info-6">Request World Info</a>
13. S -> C: <a href="/TerrariaDocs/docs/networking/packet-structure#world-info-7">World Info</a>
14. C -> S: <a href="/TerrariaDocs/docs/networking/packet-structure#request-spawn-tiles-8">Request Spawn Tiles</a>
15. S -> C: Send spawn tiles (<a href="/TerrariaDocs/docs/networking/packet-structure#send-tile-section-10">Send Tile Section</a> and <a href="/TerrariaDocs/docs/networking/packet-structure#tile-section-frame-11">Tile Section Frame</a>)
16. S -> C: Send some world state related things (TODO: Figure this out)
17. S -> C: Complete Connection and Spawn