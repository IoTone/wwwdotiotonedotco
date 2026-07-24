---
title: "BowleraramaXR — a Godot XR bowling starter for Quest 3 and Android XR"
date: 2026-06-19
draft: false
tags: ["release", "godot", "xr", "androidxr", "metaquest3", "starter"]
summary: "A synthwave-themed bowling alley doubling as a working Godot XR starter for Android XR and Meta Quest 3 — packaging the build-and-deploy steps the official docs skip."
source_url: "https://github.com/IoTone/BowleraramaXR-Godot"
repo_url: "https://github.com/IoTone/BowleraramaXR-Godot"
related_projects:
  - "bowlerama-xr-godot"
---

We published [BowleraramaXR-Godot](https://github.com/IoTone/BowleraramaXR-Godot) — a synthwave-themed bowling alley that's really a working [Godot](https://godotengine.org) XR starter for **Android XR** and **Meta Quest 3**. It ships with the [Godot XR Tools](https://github.com/GodotVR/godot-xr-tools) addon pre-installed and defaults to passthrough for glasses-class hardware, immersive for a VR HMD.

The reason it exists: getting a Godot XR project to *actually build and deploy* to a Quest is the poorly-documented part. A fresh clone that has never run "Install Android Build Template" just fails to export, and people lose hours to it. This repo commits the OpenXR vendors plugin and writes down the full, tested sequence — Godot 4.7, export templates, the build-template step everyone misses — turning the official [Deploying to Android](https://docs.godotengine.org/en/stable/tutorials/xr/deploying_to_android.html) tutorial into a Quest-specific checklist that actually works.

Requires Godot 4.7+. Source on [github.com/IoTone](https://github.com/IoTone/BowleraramaXR-Godot).
