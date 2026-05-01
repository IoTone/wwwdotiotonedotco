---
title: "Polynode launches: the missing web libraries for Snap Spectacles"
date: 2026-03-01
draft: false
tags: ["release", "spectacles", "oss"]
summary: "Spectacles-polynode ships first cut: SpaceCanvas, SpaceSVG, SpaceDOM, EventEmitter — backfills HTML5 platform APIs that Lens Studio doesn't ship."
source_url: "https://github.com/IoTone/Spectacles-polynode"
---

[Spectacles-polynode](https://github.com/IoTone/Spectacles-polynode) is open. Polynode = polyfill + node, and it provides drop-in replacements (or as close as we can get) for the HTML5 platform APIs that Lens Studio omits: 2D canvas, SVG, DOM, and a hand-ported EventEmitter. If you're trying to bring an existing JS/TS library to Snap Spectacles and the build fails on `document` or `canvas.getContext`, this is the project for you.
