---
title: "BowleraramaXR (Godot)"
date: 2026-06-19
draft: false
status: "active"
language: "GDScript"
license: "MIT"
github_url: "https://github.com/IoTone/BowleraramaXR-Godot"
weight: 19
featured: false
hero_visual: "gradient"
pill: "Godot XR"
related_news: "/news/2026-06-19-bowlerama-xr-godot/"
related_projects:
  - "gsplats-to-webxr"
summary: "A synthwave-themed bowling alley and a working Godot XR starter for Android XR and Meta Quest 3 — with the build steps that the official docs skip."
tags: ["godot", "xr", "androidxr", "metaquest3", "starter", "synthwave"]
---

## What it is

A lightweight [Godot](https://godotengine.org) project set up to run on **Android XR** and **Meta Quest 3** out of the box, wrapped in a synthwave-themed bowling alley. It ships with the [Godot XR Tools](https://github.com/GodotVR/godot-xr-tools) addon pre-installed — pointer interaction, 2D UI in 3D space, and the usual XR utilities.

For glasses-class hardware (e.g. Project Aura) it defaults to a **passthrough** experience; for a VR HMD it switches to **immersive**.

## Why it's worth having

Getting a Godot XR project to *actually build and deploy* to a Quest is the part that's poorly documented — a fresh clone that has never run "Install Android Build Template" simply fails to export, and people lose hours to it. This repo commits the OpenXR vendors plugin and documents the full, tested sequence (Godot 4.7, export templates, the build-template step everyone misses), turning the official [Deploying to Android](https://docs.godotengine.org/en/stable/tutorials/xr/deploying_to_android.html) tutorial into a Quest-specific, actually-works checklist.

## Status

Active starter. Requires Godot 4.7+. MIT-licensed; source on [github.com/IoTone](https://github.com/IoTone/BowleraramaXR-Godot).
