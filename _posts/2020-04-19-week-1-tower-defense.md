---
title: "Update #1: Starting The Project"
categories:
- Dev
feature_image: "https://picsum.photos/2560/600?image=872"
images:
  - src: /assets/img/wolf1.png
  - src: /assets/img/shark_wire.png
  - src: /assets/img/tower2.png
---

We've started working on a new project this summer. This is the first entry in a series of posts to record our progress. A lot has happened this week, and things are off to an excellent start. Let's dive into it.

<!-- more -->

## Direction

We decided fairly quickly what kind of a game we want. We wanted a simple strategy "tower-defense" sort of a game in a fantasy setting and bright cartoony art. What we couldn't decide was precisely how we were going to get that art style. Even more than that, the art we planned was more of a "thought" rather than a concrete concept. And then we found a tutorial to create a "toon shader" with Blender. That was it. That is what we want. With bold outlines and flat surfaces, it gave a hand-painted feel to the entire scene, almost like using ink and brush. Here are some very initial designs that we've done this week.

{% include slideshow.html %}

And here is a run animation for the wolf.

![wolf_run](/assets/img/wolf_run.gif)

This was also when we finally decided the setting for the game. With art like this, you either think Borderlands or calligraphy. We chose calligraphy. The game will be set against a backdrop of Japanese fantasy and folklore.

## Gameplay Code

We have already established some strong foundations for the project. We have player movement, tower placement, tower upgrades, a UI stack, a specialized input handler and an events API. Here is a little GIF showing all of that in action.

![tower-defense.gif](/assets/img/tower-defense.gif)

The player is an **AI Agent** and moves on a NavMesh on the map. While making an AI agent move is not an issue, changing the NavMesh might be. With towers being placed and moved, we would need to keep regenerating it in-game.

The tower placement indicator uses a simple spherical collider. If it collides with something, it turns red. Unity's **Layers** are quite handy for this purpose and allow you to restrict inter-layer interactions so that the selector wouldn't turn red because of the floor. Mouse clicks are handled by our input system and are just **raycasts** from the screen to the ground that also uses this layer system.

Tower upgrades are done by just destroying the old object and creating a new one in its place. These upgrades will come in the form of a skill tree that we're working on this week.

The UI stack is basically that, a stack. It will use the event system to coordinate UI screens and pass in arguments to populate UI scenes. To decouple all these UI layers, no two UI menus will directly talk to each other. They will use events to communicate with the UI system, which would then pass on that message to the relevant UI layer.

Finally, we have a basic event API to help with decoupling systems. This is basically a wrapper around Unity's **events**, which itself uses C# events delegates. The reason why we have these wrappers is to make things more convenient and also because UnityEvents with parameters are abstract and cannot be instantiated. The biggest challenge here is that C# generics don't allow variadic type parameters like C++ templates do. Because of that, we'll need duplicate events based on the number of parameters.

## Infrastructure

With any new project, some rules must be laid down for code quality. Enforcing these rules should be automated, and we've set up [Restyled](https://github.com/marketplace/restyled-io) for that. It is a GitHub app that automatically scans pull requests for code style and gives you an option to fix them automatically.

On the documentation side of things, we're using [DocFX](https://dotnet.github.io/docfx/) to generate API documentation and user guides for the project. They're hosted with GitHub Pages here.

Then we have our very own assistant, Kaka! It is a Discord bot that gives us some quality-of-life Slack features like reminders that are missing from Discord. We have a lot of plans for it though, stay tuned to see how it develops. You can find the code for it [here](https://github.com/gamedev-iitk/kaka).

An important thing that we're focusing on now is a CI pipeline. We've decided to use [CircleCi](https://circleci.com/) and will hopefully have some tests and deployments configured by the end of this week.

## Training

We've recently recruited ten new members for our team so this week was also training week. With their efforts, we've been able to prototype vital features quickly. They've been learning to use Unity, Blender and Git along with concepts like CI/CD, test-driven development, object-oriented programming, collaborating with a team on Trello etc. Based on feedback, the training process has been useful, but there are things we can do to make it even better. Essential content needs to be spread out a bit and not rushed.

## Conclusion

Overall, this has been a fantastic week for our team and a promising start for this project. The game is fully open source. You can find the code [here](https://github.com/gamedev-iitk/tower-defense) and associated documentation [here](https://gamedev-iitk.github.io/tower-defense/). Stay tuned for more updates on the game!
