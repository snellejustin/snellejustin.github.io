---
layout: post
title: "Day 3 — Game Concept: Northpole and iceblobs"
date: 2025-11-24
---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview

Today I refined my mixed reality idea into a simpler, more grounded concept.  
The game takes place inside a **North Pole research pod**, where icy blobs are trying to break in and get to your human warmth.

Your real room becomes that arctic pod.  
The walls are your lifeline, the cold is your timer, and every breach brings the temperature closer to total freeze.

---

## 1. Setting: North Pole Isolation

You’re stationed alone in an isolated research pod buried deep in the snow.  
An unknown **icy virus** has taken on physical form. It comes alive as small crawling **iceblobs** — dripping, cracking, sludge-like creatures made of frozen goo.

They want warmth.  
You are warmth.

They push through the pod’s walls, crack the metal, and crawl across the floor toward you.

---

## 2. Goal of the Game

**Try to survive by keeping the pod from freezing solid.**

### The Loop
- **Hear it:** A cracking or grinding sound forms on one of your walls in the real room.  
- **See it:** Ice spreads across the surface, and an iceblob pushes through a fracture.  
- **Stop it:** Use your **Thermal Lance** to melt it before the pod gets colder.  
- **Survive:** Each breach lowers the room’s internal temperature.

### Lose Condition
The whole room visually freezes (video passthrough turns white and icy) and the session ends (player dies).

---

## 3. How the Iceblobs Work

### What They Look Like
- Semi-transparent blue-white sludge  
- Cracked ice texture  
- Drips and chunks falling off as it moves  

### How They Enter the Room
Using MR occlusion, the enemy:
1. **Forms a bulge** behind your real wall  
2. **Cracks spread** outward on the surface  
3. A piece of the wall seems to **push inward**  
4. The iceblob **squeezes through** the fracture  

The illusion works because the occlusion mesh matches your actual walls.

### Difficulty Curve
- Early breaches take a long time to break through  
- Later breaches push through faster  
- Iceblobs move quicker and resist heat longer  
- Multiple breaches may form at once  

---

## 4. Your Tool: The Thermal Lance

Your only defense is a **Thermal Lance** — basically a concentrated heat beam.

### How It Works
- Hold trigger to fire a continuous hot beam  
- Keep it on the iceblob for ~1–2 seconds to melt it  
- As it melts(, it cracks, steams, glows, and) finally breaks apart  
---

## 5. The Room = Your Health Bar

### Temperature Indicators
- **100%:** normal passthrough  
- **75%:** subtle frost creeping on furniture edges  
- **50%:** entire room shifts blue  
- **25%:** heavy frost vignette, breathing slows, screen distorts  
- **0%:** full freeze → game over  

The more iceblobs get inside, the colder the room becomes.

---

## 6. Healing the room

To keep the game from becoming a guaranteed downward spiral, you need a way to **repair** breach damage.

### Healing Mechanic: Heat Seals

After you destroy an iceblob:
- A glowing “crack scar” remains where it came through  
- Aim the Thermal Lance at the scar  
- Hold the beam for a few seconds  
- The crack visually **melts shut**  
- Temperature increases slightly  

You’re literally welding your pod back together.

