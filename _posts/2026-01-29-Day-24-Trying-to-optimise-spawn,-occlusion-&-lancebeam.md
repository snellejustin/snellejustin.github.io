---

layout: post 
title: "Day 24 — Trying to optimise spawn, occlusion & lancebeam"
date: 2026-01-28

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview
Wednesday was a bit of a mixed bag. I tried to improve the occlusion system to make enemies hide better behind real-world objects, i also tried to make the enemies not spawn under objects such as beds and couches, but it didn't go as planned. However, I did manage to fix a really annoying visual glitch with the thermal lance effects.

---

## 1. Struggles
After adding the basic occlusion yesterday, I wanted to make it "smarter." I tried to tweak the shader to handle edge cases where the enemy would clip through the wall slightly. 
the enemies seemed to be 'stuck' in the floor, also the enemy can come through a broken piece of wall underneath an object, this all has to do with the occlusion i added yesterday.
It seems like it changed some things in the logic, but it needs to be there, otherwise you can see enemies through walls and object. I spent about 3 hours tweaking depth tests trying to fix the segmenting of the walls (who are also under objects)

**The Result:** Failed. Every change I made either made the wall invisible or made the enemy invisible at the wrong time.

---

## 2. Fixing Z-Fighting
The one win of the day was fixing the "Lance Impact" effect. When you shoot the wall, a glowing "heat scorch" decal appears.
Because this decal was spawned exactly ON the wall surface (Distance = 0), the graphics card got confused about which pixels should be on top (The Wall or The Decal). 
This caused a flickering effect known as Z-Fighting.
This issue also has to do with the new occlusion logic, but with this its mostly fixed.

**The Fix:** I added a tiny offset to the spawn logic. Now, when the raycast hits the wall, the decal is spawned 2cm (0.02f) away from the surface, along the normal.
Vector3 spawnPos = hit.point + (hit.normal * 0.02f);

---

## 3. Result
Visuals: The flickering is completely gone. The heat marks look solid and stable, even when you move your head around. The occlusion is back to the "Basic but Functional" version from Tuesday.

---

## 4. Unity

---

---

## 4. Unity
screenshot of lance impact
