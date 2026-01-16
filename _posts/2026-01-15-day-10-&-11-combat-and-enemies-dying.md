---

layout: post 
title: "Day 10 & 11 — Combat & enemies dying" 
date: 2026-01-15

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview

Over the last two days, the project took a huge leap forward.
We went from having static props to a fully functional combat loop. 
The enemies can now navigate the real world to find you, and you can fight back with the Thermal Lance.

This required solving two main technical challenges: Runtime Navigation (getting AI to walk on your floor),
and Interaction Logic (detecting hits and triggering death states).

## 1. Bringing Enemies to Life (Yesterday)
The first step was making the "iceblobs" move.
In a normal game, you bake the navigation mesh (NavMesh) beforehand. 
But in Mixed Reality, the "level" is the player's room, which we don't know until the game starts.

**Runtime NavMesh Generation**
I built a RuntimeNavmeshBuilder script that bridges the gap between the physical world and Unity's AI system.

**Wait for Scan:** The script waits for the Meta MR Utility Kit (MRUK) to finish loading the room geometry.
**Bake on Demand:** Once the room is ready, we call navMeshSurface.BuildNavMesh().
**Result:** The floor becomes a walkable surface, and furniture becomes obstacles.
With this in place, I added a NavMeshAgent to the enemies. They now intelligently pathfind around your real coffee table to get to you!

## 2. The Interaction Layer (Today)
Now that they could chase us, we needed a way to stop them.

Hit Detection I updated the lanceBeam.cs script to do more than just draw a pretty line. 
When the beam hits an object, it now checks if that object is an enemy:

enemy enemyScript = hit.transform.GetComponentInParent<enemy>();
if (enemyScript)
{
    enemyScript.Kill();
}

The Kill Logic In enemy.cs, the Kill() function handles the cleanup:

**Disable Movement:** agent.enabled = false stops the AI immediately.
**Play Animation:** animator.SetTrigger("death") plays the death animation.
**Visual Feedback:** The enemy dissolves or breaks apart (handled by the shader/animation).
This completes the core loop: Spawn -> Chase -> Shoot -> Die.

## 3. References
https://www.youtube.com/watch?v=pZ5vLcyjois&t=1574s
