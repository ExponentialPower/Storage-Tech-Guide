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
