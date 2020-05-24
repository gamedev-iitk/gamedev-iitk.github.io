---
title: "Update #4: Towers and Terrain"
categories:
- Dev
feature_image: "https://picsum.photos/2560/600?image=872"
---

Last week we focused on enemies and AI. This week we focused primarily on towers and terrain. We also refactored and modularized some systems with appropriate documentation so future developers can reuse this functionality with ease.

<!-- more -->

## Towers and AI

We implemented a ray cast based enemy detection system for the towers to give a more realistic feel to the AI. However, the ray triggered an attack as soon as the first enemy was spotted, which meant that we could not select enemies to attack. Hence, we ditched the ray casts and now use Unity's built-in `Physics.OverlapSphere`, giving us the ability to detect *all* enemies in the range at once. We then pass this list of enemies to the battle systems which select an appropriate enemy to attack.

This interaction between detection and battle systems is generic. Next week, we will refactor the enemy AI to use these components too.

With these systems in place, we were able to add the functionality of a new tower to the game. On detection, a *mine tower* places explosives near itself, damaging all enemies in its range.

## More cleanup and refactor

An essential feature that we had to improve was the tower placer. Because of the way it was creating and destroying objects, Unity raised a ton of exceptions. The problem had roots in need to distinguish between placers that move towers and placers that build new towers. We did that by just adding a boolean property and setting it on placer creation. This distinction also allowed us to implement tower movement costs in a better way.

We also made the loading of the game scene from the main menu asynchronous so that any other process that we might want to run does not get disturbed. We display the progress of this operation on a loading screen.

We also removed the hardcoded values for attack damage. Now the stats set for each character are used everywhere.

## Art and Terrain

We made significant progress with the terrain using Unity's new [Terrain Tools](https://docs.unity3d.com/Packages/com.unity.terrain-tools@3.0/manual/index.html) package. A first draft is ready that gives us a better idea of how to lay things out. The side that we need to defend is greener and more vibrant. We tried to emphasize this with a waterfall using [this](https://www.youtube.com/watch?v=XhSp8nFLUi4) and [this](https://www.youtube.com/watch?v=FbTAbOnhRcI).

![terrain.png](/assets/img/week-4/terrain.png)

We also added a catapult model into the game that will act as a simple ranged tower. This model will be animated next week.

![catapult.png](/assets/img/week-4/catapult.png)

This week has been a slow one with even slower ones queued up. But we're optimistic about the progress of the game and are looking forward to sharing it.