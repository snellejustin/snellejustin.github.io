---

layout: post 
title: "Day 27 — Tweaking the icy visor"
date: 2026-02-02

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview
Sunday was a "polish" day. I spent time actually playing the game and realized the Frost Effect didn't feel quite right. It was either too subtle or kicked in too early. I refactored the entire intensity logic to make it feel more natural and responsive to the player's performance.

---

## 1. Refactoring Intensity
The original code had a "Minimum Intensity" logic, meaning there was always a little bit of frost on the screen. The Problem: It degraded the visual clarity of the Mixed Reality pass-through. If you're doing well (0 enemies), your vision should be crystal clear.

**The Fix:**

**Removed Minimum Intensity:** If the enemy count is 0, the frost is 0.
**Adjusted Max Values:** I tuned the upper limit so that at "Critical Mass" (15 enemies), the frost is overwhelming but doesn't completely blind you (capped at 1.7 scale).
**Simplified Math:** I cleaned up the calculation logic. Instead of complex curves, it's now a cleaner linear mapping that feels more predictable.

---

## 3. Unity
screenshot of frost tuning
