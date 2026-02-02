---

layout: post 
title: "Day 25 — Atmospheric Feedback"
date: 2026-01-29

---

**Platform:** Meta Quest 3 (Unity)  
**Genre:** Mixed Reality Survival Shooter  
**Theme:** North Pole Containment / Thermal Defense  

---

## Overview

Thursday was about feedback—telling the player visually when things are going wrong. I added an Alarm System for when enemies breach, and a Frost Effect that freezes your visor as the situation gets worse.

---

## 1. The Frost Effect: Use the "Right" Way? No.

I wanted a vignette of ice to creep in from the corners of your vision. Naturally, I tried to do this the "official" Unity/Meta way. I spent an entire day wrestling with the URP Post-Processing Stack and Scriptable Renderer Features.

**The Challenge:** In Mixed Reality, getting a transparent shader to properly overlay on top of the Passthrough Layer (the real-world video feed) appereantly wasn't as easy as i thought. I watched tutorials and tried to set up a Full Screen Blit pass. Nothing worked. It was either invisible, or just didnt want to setup properly in Unity.

**The "Dumb" Solution:** After wasting hours, I deleted the entire Rendering logic and did something stupidly simple: I created a primitive Quad (a flat 3D plane), put the frost material on it, and parented it directly to the CenterEyeAnchor of the OVRCameraRig.

It literally just floats a few centimeters in front of your face. **Result:** It looks (almost) exactly the same as a fancy Post-Processing effect.

---

## 2. Alarm System

I also implemented a global visual alarm. When a wall breaks, the whole HUD flashes red and displays "BREACH DETECTED". This uses a CanvasGroup to pulse the alpha of the warning text, ensuring you don't miss the fact that a monster is walking into your living room.
I did this kind of the same way, by making the canvas float infront of the player's eyes.

---

## 3. Unity

screenshot of frost effect

---

## 4. Resources

https://www.youtube.com/watch?v=mCpRxFP2J1c
https://www.youtube.com/watch?v=mNpC6nB4uFM

---
