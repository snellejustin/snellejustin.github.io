---

layout: post 
title: "Day 23 — Breaching of enemies & occlusion shader"
date: 2026-01-27

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview
Tuesday was all about making the "Invasion" feel real. Up until now, enemies just spawned in the room (or in the void). 
I wanted them to actually feel like they were coming from the cold outside into your warm room. This required a complete rewrite of the spawning logic and some shader magic.

---

## 1. The Breach Mechanic
I moved the enemy spawning logic into the DestructibleGlobalMeshManager. Now, the destruction of a wall and the spawning of an enemy are linked events.

**The Logic:**

A wall segment breaks (opening a hole).
The code calculates a vector from the Player to the Wall.
It extends this vector 4 meters outward (behind the real wall).
It spawns the enemy there and tells it to walk through the new hole.
The Result: the wall breaks, and you see an enemy coming at you from the snowy void outside. It's much simpler but way more immersive than just fading them in.

---

## 2. Refactoring Spawning
Previously, I had a separate EnemySpawner script that just picked random spots. It was messy and didn't know about the walls. By moving this into the DestructibleManager, I can control exactly when and where enemies appear. No more enemies spawning inside furniture or floating in the ceiling. They always come from a breach.

---

## 3. URP Occlusion Shader
To make this work visually, I needed a way to hide the enemies while they were still "behind" the unbroken walls. In Mixed Reality, the "real" wall isn't a digital object, so it doesn't automatically block virtual objects.

**The Solution:** I added created a URP Occlusion Shader. This is a special material that checks the "Depth Buffer" but renders nothing (invisible). I applied this to the invisible room mesh.

**Result:** It acts like a "Collision Mask" for light. The real-world wall now correctly "hides" the virtual enemy standing behind it. The enemy only becomes visible when it steps through the hole (where the occlusion mesh is removed). Same with object such as tables, couches and everything else that is scanned before playing.

---

## 4. Unity
screenshot of enemy breaching
