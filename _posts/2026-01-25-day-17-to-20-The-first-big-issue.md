---

layout: post 
title: "Day 17 to 20 — The first big issue"
date: 2026-01-20

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview

I spent a few days stuck on a really annoying issue. I was trying to get the enemies (blobs) to spawn from the walls using the room scan data. The code looked fine, the logic was there, but nothing was showing up in the game.

---

## What I Tried

I checked pretty much everything I could think of:

I checked if the prefabs were null.
I checked if they were spawning inside the walls or at the wrong coordinates.
I messed with the materials and shaders to make sure they weren't just transparent.
I checked the camera layers.
I even made them huge just in case they were too small to see.
The strange part was that the i didnt get any warnings or errors, even when focusing on different parts of the game nothing changed.
that's when i knew it wasn't a mistake in the code, but something general. which made it harder to solve, no one on the internet could help me and ai also didn't give a clear explenation, ai was just guessing stuff that i know didn't have anything to do with my issue

---

## The Fix

I decided to go over ALL of my settings to see if there was something strange, 
it turned out to be something really simple. I was just in the wrong scene.
This must have happened when my Unity crashed and opened a recovered scene instead of the one i was actually loading in my meta quest.

---

I was editing the scripts and prefabs in the SampleScene, but whenever I hit Play in Unity, it was loading a recoveredScene I had open. So the code was technically running, but it was spawning objects in a completely different scene than the one I was looking at.

---

## Lesson Learned
Always check which scene is actually active. I assumed I was testing my changes, but I was looking at an empty scene the whole time.

---



