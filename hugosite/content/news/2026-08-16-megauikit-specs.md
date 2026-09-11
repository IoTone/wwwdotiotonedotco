---
title: "MegaUIKit — summoning the Specs sample library out of mid-air"
date: 2026-08-16
draft: false
tags: ["release", "spectacles", "ar", "uikit", "lens-studio", "typescript", "ui"]
summary: "A holographic floor menu for Snap Specs that discovers the Essentials template's fourteen sample groups at runtime and lets you summon any of them without leaving the headset — three switchable skins, built on UIKit rather than around it."
source_url: "https://github.com/IoTone/MegaUIKit-SPECS"
repo_url: "https://github.com/IoTone/MegaUIKit-SPECS"
related_projects:
  - "megauikit-specs"
---

Snap's **Essentials** template for Specs ships fourteen sample groups — Solvers, Instantiation, InteractableHelper, Raycast, Collision, Mini Demos and the rest — laid out as top-level scene objects, most of them disabled. Browsing them means hunting through the Scene Hierarchy panel, toggling one on, toggling it off, and repeating. [**MegaUIKit**](https://github.com/IoTone/MegaUIKit-SPECS) replaces that loop with a **holographic floor menu** you can use from inside the headset.

A board sits about a foot off the ground, tilted back so it never occludes what it summons, one tile per sample group. Look at a tile and it lifts and brightens, with a spinning 3D title floating above it. Pinch it and its examples unfurl as a menu in a frame you can drag anywhere. Pinch an example and it materialises into the scene. Pinch again to dismiss. Opening anything closes whatever was open before — without that rule the scene silts up with five samples fighting for the same volume of air and no way to tell which behaviour belongs to what.

Three skins — **Terminal** (cyberpunk), **Gilded** (steampunk) and **Neon** (Neo-Tokyo) — each with its own palette, typeface, motion language and sound, switchable from inside the scene.

## Design notes worth stealing

**Nothing about the sample library is hardcoded.** The menu builds itself by walking the live scene; disabled objects are still present in the hierarchy, so a dormant sample is fully enumerable even though none of its scripts have ever run. Add or rename a group in the Editor and the menu picks it up next launch — no manifest.

The catch, learned the hard way: **runtime roots are not authored roots.** By the time the menu builds, packages and editor tooling have added scene roots of their own. The first build listed 18 groups instead of 14 and its clean-scene pass silently disabled the MCP preview agent. Roots are now filtered by naming convention and by having at least one child.

**UIKit does the interaction; the skin is a layer on top.** Tiles and rows are UIKit `Button`s, not hand-rolled quads — which buys the hover/press state machine, auto-fitted colliders, gaze and pinch targeting, and SnapOS theming for free. That's the difference between a menu that *looks* like Specs UI and one that *behaves* like it.

**Themes are data, with an escape hatch.** Every colour, radius, easing name, stagger time, font and sound lives in a `MenuTheme` object. Three behaviours genuinely resist being data — Terminal's character corruption, Gilded's hinge tilt, Neon's bloom — and those are named by enum and branched on, rather than pretending a field could describe them.

**Live inputs come from reflection.** `Object.keys` on a `ScriptComponent` returns its `@input` fields and writes to them stick, so an active sample's boolean inputs appear as toggles you can flip while it runs — no author-time manifest. The limits are stated plainly in the README: a script that reads its inputs once in `onAwake` will ignore the edit, and `@hint` text and numeric ranges exist only in the Editor API, which is why it's booleans-only for now.

Requires Lens Studio 5.22+. Target platform is Spectacles; there is no Snapchat-camera path. Source on [github.com/IoTone/MegaUIKit-SPECS](https://github.com/IoTone/MegaUIKit-SPECS).
