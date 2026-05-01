---
title: "Spectacles-polynode"
date: 2026-03-01
draft: false
status: "active"
language: "TypeScript"
license: "MIT"
github_url: "https://github.com/IoTone/Spectacles-polynode"
weight: 5
featured: true
hero_visual: "gradient"
pill: "Lensfest 2nd Place 2026"
award: "Lensfest March 2026 — 2nd Place OSS Prize · Snap Inc. + Lenslist"
related_news: "/news/2026-03-30-polynode-wins-2nd-place-lensfest-march-2026/"
related_projects:
  - "spectacles-matematex"
  - "spectacles-skywriter-ble"
  - "snap-spectacles-ik-samples"
summary: "The 'missing' web utility/core libraries for Snap Spectacles — SpaceCanvas, SpaceSVG, SpaceDOM, EventEmitter — backfills HTML5 platform APIs Lens Studio doesn't ship."
tags: ["spectacles", "ar", "lens-studio", "polyfill", "typescript"]
---

## What it is

Polynode = polyfill + node. It backfills HTML5 platform APIs that Lens Studio doesn't ship — DOM, 2D Canvas, SVG, EventEmitter — so existing JS/TS libraries can be ported to Snap Spectacles without rewriting from scratch.

## Modules

**SpaceCanvas** is a drop-in replacement for HTML5 canvas. It uses the WebView and a few patterns the Snap team shared on the Reddit forums. There are 4 samples: a general gallery, something resembling Snakes, a bad shooter, and Conway's Game of Life. SpaceCanvas runs hot — WebViews overheat the Spectacles thermals — so a tuning pass is scheduled.

**SpaceSVG** is the gem. It converts SVG strings into meshes that look nice and run efficiently. It isn't fully spec-compliant but it's solid enough to render 2D shapes, illustrations, and animations. SpaceSVG is what made the LaTex port (Matematex) viable.

**SpaceDOM** is a minimal DOM shim — alpha — useful when you're trying to get a library to even compile in Lens Studio. Bug reports welcome.

**EventEmitter** is a hand port of node's pattern, used across IoTone's lenses for clean inter-script messaging.

## In production

Used by [Spectacles-Matematex](https://github.com/IoTone/Spectacles-Matematex) for math notation in AR, the [Moire Lens Lab](https://github.com/IoTone/www-moirelenslab) art-book project, and several IoTone Japan client builds.

## Roadmap

SpaceCanvas thermals tuning · SpaceSVG spec-compliance pass · SpaceDOM beta with worked examples · LaTex 1.0 release on Matematex.
