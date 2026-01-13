---

layout: post 
title: "Day 9 — Bringing Enemies to Life: AI and Navigation" 
date: 2026-01-13

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview
Today, the "iceblobs" evolved from static spawns into active threats.
To make them chase the player, I needed a way for them to navigate the physical room. This is tricky in Mixed Reality because we don't know the room layout until the game starts.

I solved this by generating a Navigation Mesh (NavMesh) at runtime, using the data scanned by the Quest 3.

## 1. The Challenge: Navigation in Mixed Reality
In a standard game, you "bake" the NavMesh (the walkable floor area) in the Unity Editor.
In Mixed Reality, the "level" is the player's living room, which changes for every user.

**We need a system that:**

-Waits for the room scan to load.
-Identifies the floor and obstacles (tables, couches).
-Generates a NavMesh on the fly.

---

## 2. Runtime NavMesh Generation

I created a script called RuntimeNavmeshBuilder to handle this dynamic baking.

**How It Works**
Integration with MRUK: The script registers a callback with the Meta MR Utility Kit (MRUK). It waits for the SceneLoaded event, which fires once the Quest has finished scanning and loading the room geometry.
Building the Mesh: Once the scene is ready, it calls navMeshSurface.BuildNavMesh(). This function (from Unity's AI Navigation package) analyzes the newly created room mesh and calculates where agents can walk.
Result: The real-world floor becomes a valid pathfinding surface, and furniture becomes obstacles that enemies must walk around.

---

## 3. Enemy AI
With the NavMesh in place, I added a simple brain to the enemies using enemy.cs

**NavMeshAgent:** Each enemy has a NavMeshAgent component. This handles the physics of moving along the NavMesh.

**Targeting:** In the Update loop, the enemy constantly sets its destination to Camera.main.transform.position (the player's head).
Chase: The agent automatically calculates the shortest path around obstacles to reach the player.
Now, if you hide behind your real-world couch, the iceblobs will actually have to pathfind around it to get to you!

## 4. Unity
///

## 5. References
https://www.youtube.com/watch?v=pZ5vLcyjois&t=1574s
