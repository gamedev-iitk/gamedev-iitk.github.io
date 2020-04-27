---
title: "Week 2: CI, Health and More"
categories:
- Dev
feature_image: "https://picsum.photos/2560/600?image=872"
---

This was a much more code-focused week than the last one. We've completed a variety of new features. Let's look at them in detail.

<!-- more -->

## Automation

While we're not new to the topic of continuous integration, implementing that with Unity did pose some challenges. First of all, how do we install Unity on our runner? Fortunately, after some research, we found an excellent guide that everyone seemed to follow - [using GitLab CI with Unity by gableroux](https://gitlab.com/gableroux/unity3d-gitlab-ci-example). The solution to the installation problem? Use Docker! The guide also mentions ways to solve licensing issues and activating your editor without the Unity Hub.

Now, GitLab worked great, but it isn't that well integrated with GitHub, and we don't want to migrate our code right now, so we went with [CircleCI](https://circleci.com/). With their friendly documentation and some help with [this article](https://medium.com/@neuecc/using-circle-ci-to-build-test-make-unitypackage-on-unity-9f9fa2b3adfd), we could port the same GitLab functionality over to CircleCI. The benefits are better GitHub integrations (like tests for pull requests and status checks) plus more options to optimize our workflows down the line. With this pipeline in place, we can now continuously test our product and quickly identify bugs. We're currently working on automating our documentation through this too.

Another nifty piece of automation that we have now is a little GitHub Issues Trello sync. Basically, creating an issue triggers a GitHub Action that runs a python script to create a new card on our project board through an HTTP request. Neat!

## Gameplay

On the gameplay side of things, we now have health and attacks! For now, all towers have a spherical trigger to act as detection range. We use `OnTriggerEnter` and `OnTriggerExit` to look for enemies and attack them. Rotating the tower happens with the built-in `Quaternion.LookRotation` function and some linear interpolation to smoothen it out. This is not the best solution because if a tower kills an enemy and they're destroyed, `OnTriggerExit` is not called. There needs to be something like a `ScanEnemy` function that we can call anytime and reassign targets based on some conditions.

![tower-target.gif](/assets/img/week-2/tower-target.gif)

We also have an upgrade hierarchy now, using dictionaries by [azixMcAze](https://github.com/azixMcAze/Unity-SerializableDictionary). Unity cannot serialize dictionaries on its own, so we needed a third-party solution. Using this tool, we assign booleans to tower types. For example, green can turn into red but not gold, so we'll assign `red:true` and `gold:false` to the Green tower's prefab. This is stored by the `UpgradeTree` component.

![upgrade.png](/assets/img/week-2/upgrade.png)

Finally, we need to start work on enemy AI and the wave system. But before we can do that, there is a little problem. Video games use an asset called a [*navigation mesh*](https://en.wikipedia.org/wiki/Navigation_mesh) for pathfinding. It splits your map into convex polygons (the mesh) and connects those polygons to form a graph structure. This marks parts of the level which are traversable and which are not. In our game, the player will always be placing and moving towers. Therefore, this mesh needs to be updated anytime a tower is placed. Otherwise, AI characters will try to move through the tower. But this really seems like something games do all the time, so Unity should have something built-in? Yes, it does! Using the [Nav Mesh Obstacle](https://docs.unity3d.com/Manual/class-NavMeshObstacle.html), we could implement this functionality pretty quickly.

## Plans

Looking back at these two weeks, we're moving at a consistent pace and should have a completely playable prototype soon. After that, it is all about squashing any remaining bugs. Things on the art side are moving pretty slow, but iteration is essential. Get a simple concept complete first and then work on improving it.

This coming week we'll like to have some of our own art assets implemented in the game and start on creating a map. On the code side, we'll continue to work on the enemy AI and the wave system.

**Thank you for reading!** If you want more details please visit our [project](https://github.com/gamedev-iitk/tower-defense) or the [documentation](https://gamedev-iitk.github.io/tower-defense/).