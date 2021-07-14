---
layout: default
---

# Battle RPG demo

The Isometric Battle RPG was a short project I did to show my pathfinding, realtime navigation mesh generation and AI skills. It is a top down, turned based game inspired by D&D and XCOM - XCOM esspecially as it provided the basis for the grid based map and action based combat system. You can check it out for yourself on my [GitHub page](https://github.com/Liam-Harrison/Battle-RPG-Demonstration).

![RPG Demo](https://i.imgur.com/b5rxKD9.png)

The idea originally was to have a deep simulation underneath the graphics and the game would be text based - basically Zork but with 3D feedback. But despite making the simulation component to support a 3D Zork game I thought it would be better to make a more modern XCOM inspired combat system.


## Real time automatic navigation mesh generation

The navigation mesh system I developed was specific to my games design, it dynamically and automatically generates a navigation mesh at runtime, it can be altered, saved, loaded, and update specific parts of itself (say if a path is created or blocked).

![RPG Nav Mesh](https://i.imgur.com/bLLu6Tx.png)

The weights of the nav graph are considered when pathfinding and automatically generated depending on parameters, you can set a max height where connections will no longer join nodes together, these weights also allow the AI agents to do special actions, such as jumping large gaps if they are allowed to - The nav mesh is also very quick to generate, the output from the most recent build was the following:

```
Generated 796 nodes with 1491 connections on 10 enviormental objects in  150 milliseconds.
```

## Intuitive, fast & asynchronous pathfinding.

The AI is tightly coupled to the navigation mesh, and can use it to find the best path from one position to another using the A Star graph traversal algorithm. 

[![RPG Pathfinding](https://i.gyazo.com/f33b4905a397ab49fb69b9dce7bb0be9.gif)](https://gyazo.com/f33b4905a397ab49fb69b9dce7bb0be9)

The algorithm currently uses a basic heuristic that only measures the absolute distance between the entity and the desintation, further improvments could be made to greatly speed up pathfinding - such as seperating nav mesh zones and connecting them with known paths which would mean the entity would not need to calculate a path from its position to the destination, just from its position to the next zone connection.

## A deep combat system

The combat system allows each entity to use action points to execute actions, actions can include anything from a move to an attack. Actions are quick to design and easy to implement, creating a new action is as easy as setting up the meta data, writing a short script, and adding that action to an entity/entities.

![Action system](https://i.imgur.com/6hm5eVh.png)

### [Public GitHub Repository Link](https://github.com/Liam-Harrison/Battle-RPG-Demonstration)

### [Return to the homepage](./)
