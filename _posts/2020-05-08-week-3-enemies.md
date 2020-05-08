---
title: "Week 3: Enemies"
categories:
- Dev
feature_image: "https://picsum.photos/2560/600?image=872"
---

This week we implemented the bad guys. Read on for details.

<!-- more -->

## Enemy AI

As noted in the previous article, the collider based enemy detection wasn't a great solution. We now use raycasts for detection. Each tower has a "radar", that is, a ray sweeps some area and attacks the first enemy it finds. This makes things very flexible for us and allows towers to behave more naturally.

For the actual enemy AI, we wanted a standard behaviour-tree based implementation. It made sense to have a general behaviour-tree as a standalone package that we can use for future games. We looked at [xNode](https://github.com/Siccity/xNode) and an [OpenWorldAI](https://bitbucket.org/EngiGamesBitbucket/engigames_aiproject/src/master/) project for reference. It became apparent that this was not going to be a trivial task. So a general implementation is now on hold, and we've added character-specific behaviour to our project as standard scripts. We have two enemy types for now - the berserker that destroys everything in its path and the runner that dodges everything in its path.

Finally, we completed the wave system. Enemies now spawn in waves, and there is a cooldown between waves to help players prepare. We also have bonus waves every now and then for extra resources and tougher enemies.

![wave.png](/assets/img/week-3/wave.png)

## User Interaction

We've added a simple pause menu and the main menu. Having a structure like this makes it feel more like a "real game". Most buttons don't do anything for now, but we'll continue to hook them up to real gameplay systems in the coming weeks.

![main_menu.png](/assets/img/week-3/main_menu.png)

We've also added a wallet visible on the HUD. Players need to spend this money to create, upgrade and move towers. With this, the most basic gameplay systems are now in place. We need to make these systems interact with each other in better ways and start changing all cubes into actual characters.

![upgrade.png](/assets/img/week-3/upgrade.png)

## Tools and Logistics

Users can now report bugs directly from the game. We're using [Unity Cloud Diagnostics](https://unity3d.com/unity/features/cloud-diagnostics) to capture application state for bug reports. This will make tracking bugs easier and help us fix them faster.

And finally, our Discord bot is now live! Kaka is hosted on Heroku and will eventually provide some much-needed integrations between GitHub and Discord.
