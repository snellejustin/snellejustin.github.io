---

layout: post 
title: "Day 21 — Cooldown Mechanics & Polish"
date: 2026-01-25

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview
Sunday was a big day for mechanics. I finally implemented a proper heat/cooldown system for the lance so you can't just spam it forever. 
I also refactored the entire welding logic because the old one was a mess, and fixed a 4-day long bug where I couldn't see the UI.

---

## 1. The Heat Mechanic
The Thermal Lance is a powerful weapon, but it needed a downside. I added a heat system that builds up as you fire.

**Heating Up:** Firing adds heat over time (takes 5 seconds to max out). 
**Overheat:** If you hit 100% heat, the weapon jams. You have to wait for it to fully cool down (0%) before you can shoot again. 
**Visuals:** I added a new Cooldown UI on the HUD. The bar goes from Yellow to Red as it gets hotter.

---

## 2. Refactoring Welding
The old welding code was barely working. It had trouble identifying which wall you were trying to fix. 
I rewrote the target identification logic (
GetHitboxFromObject
) so it's super reliable now. 

**The Fix:** I also decoupled the UI from the wall objects. Now the code reliably tracks exactly how long you've been welding a specific hole and updates the UI accordingly, the UI now floats in front of the players eyes.

**Visuals:** I also changed how the target to 'weld' the hole looks, it now displays a welding icon so the player knows why to hit the orange icon.

---

## 3. Result
Current State:

You have to manage your heat while shooting enemies.
If a wall breaks, you can reliably repair it with the new progress bar.
The UI actually shows up now.

---

## 4. Unity
screenshot of cooldown ui
