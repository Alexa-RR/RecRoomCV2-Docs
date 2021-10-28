---
title: 'CV2 execution types'
order: 2
---
In CV2, there are two basic execution types: 

1. Chips with an exec input port execute when an exec signal arrives at that port.

2. Chips without an exec input port (auto-)execute "on demand" when another chip reads data from their output ports.

In addition to these two basic execution types, there are different ways circuits are executed as soon as there is more than one player in a room instance as discussed next.

## Local execution
In principle, all circuits are executed "locally" on the machine of an individual player, i.e., their PC, phone, tablet, console, etc. 

## Synced execution
To execute a circuit on the machines of all players in a room instance, you can send a synced event to all players. An event receiver will then fire an exec signal for all players at about the same time. While these executions start synced, the control flows can quickly desync for different players, for example, because unsynced variables have different values for them.

## Synced effects
Even if the execution itself is not synced, the effects of executed circuits may be synced. For example, many variable chips have an option to be synced. For synced variables, a single player can set a new value, which is automatically synced for all other players in the same room instance. Most gizmos and gadgets are synced by default; i.e., even if just a single player changes their properties, that effect is synced for all other players. Some gadgets (e.g. Text V2, Pointlight V2, Spotlight V2, or SFX V2) have the option not to be synced such that they can appear differently for different players. 

Sometimes the automatic syncing of gadgets can cause problems. For example, if all players set properties of a synced gizmo, there will be a lot of syncing messages between players and the gizmo will try to sync itself for all players based on syncing messages from all players, which can result in juddering motions. In this case, it is better to let only one player set the proporties of the synced gizmo (usually the player who has authority over the gizmo or the room instance), and let the automatic syncing make sure that the other players see a similar motion.

In other cases, it is preferable to turn off the automatic syncing and "manually" sync gadgets by synced events that set their properties. For example, the automatic syncing of the text of a Text V2 gadget can result in too many syncing data if the text is changed very often, e.g., for the display of a timer or clock. In this case, the text of an unsynced Text V2 gadget could be set in a synced event such that all players see the same text without the expensive syncing of the Text V2 gadget.
