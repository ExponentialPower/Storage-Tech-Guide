# Lag
---
## Explanations of the various kinds of lag and what causes them. There are many good/bad practices you can use to avoid lag that are covered here.
---

### Hoppers

Hoppers are essentially the laggiest block in Minecraft. This is mainly due to their ability to suck item entities from the air. This requires the hopper to constantly check  for any item entities which is quite an expensive process for the game. To stop this lag, the hopper can be powered or “locked”, and this basically short-circuits the hopper’s operations and prevents them from causing much of their lag.

![Simple Hopper Tick Flowchart](https://cdn.discordapp.com/attachments/756677711111389236/834133822199169044/unknown.png)
_Chart by Cubicmetre_

The chart above is a simplified version of all the steps a hopper goes through in a single tick. As you can see, when the hopper is enabled (unlocked) there are far more steps to check than when it is locked (powered). Therefore, locking hoppers is a simple yet extremely effective way to reduce lag. But, what if you need hoppers to be able to move items constantly? Most hopperlocking systems only unlock the hoppers when the system is running. However, sometimes hoppers need to remain unlocked so they can always transfer items. The main cause of lag by hoppers is checking for item entities in the block above them each tick. There is a simple way to prevent this and still allow items to flow through. As shown by the chart above, the step to check for item entities can be avoided if there is a container above which can be pulled from instead. The least laggy option to use as a container is a composter. This is because of two main reasons: 1) Compostors only have a single inventory slot which can only contain bonemeal, making it simple to check the contents. 2) Compostors are not tile entities and therefore cause less lag (See ___Tile Entities___). A standard block will not reduce the lag caused by a hopper, as the hopper can still pick up item entities that manage to end up inside the block. This can be proved by these tests:  Point a dropper into a solid block with a hopper underneath, then trigger the dropper. The item entity should be spawned inside the block and collected by the hopper. If you place a compostor over a hopper and throw an item into the compostor, the item  will not be collected because the hopper is searching for bonemeal in the compostor and not checking for entities.

![Hopper Lag Tests](https://cdn.discordapp.com/attachments/756677711111389236/839539969990459402/hopper-lag-reduction-test-chart-image.png)
_Tests by ExperimentalIdea_

As shown by the above testing, compostors are the least laggy block to put on top of a hopper aside from a redstone block, which locks the hopper. From there, the number essentially increases by the number of inventory slots in the container above. The exceptions to this are the various kinds of furnaces which cause unnecessary lag because they are ticking entities.



---

### Redstone Dust

Redstone dust is one of the laggiest components while powering, depowering, or changing signal strengths (ss). It also changes a lot between versions. This information is up to date with the current version at time of writing [1.18]. Statically it does nothing, but dust creates twenty-five block updates per “step” it changes. While powering, connected redstone dust blocks complete the signal strength change instantly, with each of the connected dust going up a single “step”. Even with only two dust, that is equal to 50 updates for a 0 to 15 signal strength change. Depowering, connected dust goes down in steps of two until the final level is reached. For example, if there is a dust at ss10 and it depowered to ss5, it would step down first to 8, then 6, and finally 5. Even though this happens in the same tick, it still sends the block updates at each step. This causes a lot of updates when depowering connected dust. If you were to have a line of only two dust and power one of them with ss15, it would create a total of fifty block updates between both of them. If you removed the power source, that would cause _425_ updates. That is only for two dust. It is easy to see how this can increase as you link dust together. A single piece of unconnected dust instantly unpowers the same as it powers in only one step, making it much more acceptable. The only main reason dust is used (outside of single dots) is for encoding in hexadecimal due to the fact that it has sixteen possible states. Something that is better suited for transmitting signals long distances is a combination of observers and rails which can be used to simpler effect.



---
### Droppers
Droppers cause minor lag by being a tile entity, but their main lag comes from moving items between containers or dropping items into the world. When moving an item into a container, the dropper needs to select a random slot, then check if the item contained in that slot fits in any of the slots in the other container. It can go through up to 54 slots, checking each one, if there is a dropper pointing into a full double chest. When dropping an item into the world, the dropper needs to choose a random slot, spawn an item entity, and choose random velocities in all three dimensions. This is the most laggy process as the calculation of momentum is an expensive process for the computer and the spawned itme entity creates its own lag, being an entity.



---
### Tile Entities
Tile entities(TE) are any block that contains an inventory, or anything that requires more information stored than the block states you see under 'block info' on the f3 screen. Things that are stored in block states are simple values, like the number of sea pickles or candles in a block, or the lit status of a redstone torch. More complex information, like the quantity and type of each item stored in a double chest are stored in a TE, which is more complex and creates more lag. Other tile entities that are less intuitive to see are things like signs and moving pistons. Signs need to store the text input, color, and whether or not there is glow ink applied. Some aspects of a block that is also a TE are still stored in block states like the open status of a barrel or shulker. Moving piston TEs store the blocks being moved, start position, and end position, and are the main reason TEs cause lag.



---
### Pistons
Pistons are laggy for a few main reasons. Statically they cause the same lag as a normal block, but when the piston moves, it creates a tile entity(TE) for the moving blocks. The TE itself isn't bad, but the game needs to add and then remove it from a list of all the TEs in that chunk. (In versions 1.17- the TE list is stored for the entire world instead of per chunk, causing far more lag from pistons) For example, if you power a piston in an empty chunk, it will cause far less lag than in a chunk filled with other TEs, such as droppers. Therefore it is good practice to reduce the number of pistons, and try to keep them out of the same chunk. Another issue is that when a piston or the blocks it is pushing extend across a chunk border, the TE is created in two chunks and creates lag for both of them. There isn't usually much that can be done about putting pistons and TEs in the same chunk, so it is best to just try and reduce the number of TEs all together. Something that can be done when building a full storage system is to chunk-align some components to reduce the number of pistons that cross chunk borders.
