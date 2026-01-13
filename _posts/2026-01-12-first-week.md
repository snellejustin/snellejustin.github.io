---

layout: post 
title: "week 1 — Mechanics: Welding, Shooting, and Spawning" 
date: 2026-01-12

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview
Over the last few days, I moved from concept to concrete implementation.
I focused on the core interaction loop: firing the Thermal Lance and spawning enemies.

The goal was to make the shooting feel responsive and satisfying ("welding" the room) and to ensure enemies spawn intelligently on the actual walls of the player's room.

---

## 1. The Thermal Lance (Hold-to-Shoot)
The first step was refining the shooting mechanic.
Initially, the beam was a simple toggle. I changed this to a hold-to-shoot system to mimic the feeling of operating a heavy industrial tool

**Input Handling**: Used OVRInput.GetDown and GetUp to track the trigger state.
Continuous Update: While the button is held, the beam's position updates every frame to follow the controller.
Audio Sync: The "welding" sound loops only while firing and cuts off immediately upon release, making the tool feel responsive.

---

## 2. Visual Feedback: The "Welding" Effect
I wanted the player to feel like they were physically heating up the walls.
Simply spawning a particle effect every frame was too performance-heavy (60+ objects per second!), and spawning just one object didn't leave a trail.

**The Solution**: Distance-Based Spawning

I implemented a system that draws a trail of heat marks based on movement distance, not time.

**Track Position**: The script remembers the lastHitPosition of the beam.
Check Distance: Every frame, it calculates the distance between the current hit point and the last one.
**Spawn**: If the beam has moved more than 0.05 units, it spawns a new heatImpact prefab.
**Cleanup**: Each mark destroys itself after 1 second.
This creates a smooth, continuous "weld" line that looks great but stays performant.

---

## 3. Enemy Spawning (MR Utility Kit)
To make the "iceblobs" feel like they are breaking into the room, they need to spawn on the walls, not just in mid-air.

Using Meta MR Utility Kit (MRUK)
I integrated the Meta MR Utility Kit to leverage the scene understanding capabilities of the Quest 3.

**Room Awareness**: The enemySpawner script now references MRUK.Instance.GetCurrentRoom().
Wall Finding: I used GenerateRandomPositionOnSurface with SurfaceType.VERTICAL to find valid spots on the walls.
Label Filtering: We can filter by labels (e.g., WALL, WINDOW) to control exactly where enemies can breach.
Now, enemies pop out of the actual physical walls of my living room! (still in progress since this is the last thing i added)

---

## 4. Project Hygiene
As the project grew, the repository got cluttered. I took some time to clean up the Git history.

**Gitignore**: Added rules to ignore build artifacts, crash dumps, and library folders.
Repo Structure: Removed nested repositories to keep the history clean and linear.

---

## 5. Unity
**Understanding the UI**: Since the Unity software is completely new to me it took me some time to get used to it. I'm following tutorials
on youtube in which the 'teacher' explains what he's doing very well, but it ofcourse still takes time to remember where to find certain buttons or different tabs.
Up until now i haven't had many setbacks, let's hope it stays that way!

**Macbook 'struggle'**: Since Mac isn't prefered in the development of meta quest apps i have experienced a few cons. Such as testing out parts of the game:
I have to either run a simulator or build the whole app, this takes some time but for now it's managable. Using a cable connection makes the build go faster.
Once the game grows and the builds take longer, i might have to reconsider how to approach this.

---

## 6. References
https://www.youtube.com/watch?v=pZ5vLcyjois&t=1574s --> 2,5h long tutorial that explains the basics of make a meta quest game in unity
Unity Docs & Meta Docs
