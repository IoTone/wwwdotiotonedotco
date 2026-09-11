---
title: "MegaUIKit for SPECS"
date: 2026-08-16
draft: false
status: "active"
language: "TypeScript"
license: "MIT"
github_url: "https://github.com/IoTone/MegaUIKit-SPECS"
weight: 21
featured: false
hero_visual: "alt-2"
pill: "Specs UI"
related_news: "/news/2026-08-16-megauikit-specs/"
related_projects:
  - "spectacles-deskwindow"
  - "spectacles-polynode"
summary: "A holographic floor menu for Snap Specs that discovers the Essentials template's fourteen sample groups at runtime and summons any of them without leaving the headset. Three switchable skins, built on UIKit rather than around it."
tags: ["spectacles", "ar", "uikit", "lens-studio", "typescript", "ui"]
---

## What it is

Snap's **Essentials** template for Specs ships fourteen sample groups laid out as top-level scene objects, most of them disabled. Browsing them means hunting through the Scene Hierarchy panel, toggling one on, toggling it off, and repeating.

MegaUIKit replaces that loop with a **holographic floor menu**. A board sits about a foot off the ground, tilted back so it never occludes what it summons, one tile per sample group. Look at a tile and it lifts and brightens with a spinning 3D title above it. Pinch it and its examples unfurl in a frame you can drag anywhere. Pinch an example and it materialises into the scene; pinch again to dismiss.

Three skins — **Terminal** (cyberpunk), **Gilded** (steampunk) and **Neon** (Neo-Tokyo) — each with its own palette, typeface, motion language and sound, switchable from inside the scene.

## Design approach

**Nothing about the sample library is hardcoded.** The menu builds itself by walking the live scene. Disabled objects are still present in the hierarchy, so a dormant sample is fully enumerable even though none of its scripts have run. Add or rename a group in the Editor and the menu picks it up next launch — no manifest to maintain.

The catch, learned the hard way: **runtime roots are not authored roots.** By the time the menu builds, packages and editor tooling have added scene roots of their own — the first build listed 18 groups instead of 14, and its clean-scene pass silently disabled the MCP preview agent. Roots are now filtered by naming convention and by having at least one child.

**UIKit does the interaction; the skin is a layer on top.** Tiles and rows are UIKit `Button`s, not hand-rolled quads, which buys the hover/press state machine, auto-fitted colliders, gaze and pinch targeting, and SnapOS theming for free — the difference between a menu that *looks* like Specs UI and one that *behaves* like it.

**Themes are data, with an escape hatch.** Every colour, radius, easing, stagger time, font and sound lives in a `MenuTheme` object. The three behaviours that genuinely resist being data — Terminal's character corruption, Gilded's hinge tilt, Neon's bloom — are named by enum and branched on, rather than pretending a field could describe them.

**Live inputs come from reflection.** `Object.keys` on a `ScriptComponent` returns its `@input` fields and writes stick, so an active sample's boolean inputs appear as toggles you can flip while it runs. Two honest limits: a script that reads its inputs once in `onAwake` ignores the edit, and `@hint` text and numeric ranges exist only in the Editor API — which is why it's booleans-only for now.

**One thing at a time.** Activation is exclusive; without it the scene silts up with five samples fighting for the same volume of air.

## Status

Active. Requires Lens Studio 5.22+. Target platform is Spectacles — there is no Snapchat-camera code path. Source on [github.com/IoTone/MegaUIKit-SPECS](https://github.com/IoTone/MegaUIKit-SPECS).
