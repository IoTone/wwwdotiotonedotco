---
title: "MusicPixels (Cardputer ADV)"
date: 2026-07-18
draft: false
status: "active"
language: "C++"
license: "MIT"
github_url: "https://github.com/IoTone/CardputerADV_Hacking_Japan"
weight: 26
featured: false
hero_visual: "alt-2"
pill: "Open hardware"
related_news: "/news/2026-07-18-cardputer-musicpixels/"
related_projects:
  - "midi-bleep-blop"
  - "openwr"
summary: "A generative analog-style synthesizer for the M5Stack Cardputer ADV, with audio-reactive geometry drawn on a transparent M5 Unit Glass OLED. Out of the Fukuoka hacking scene."
tags: ["m5stack", "cardputer", "hardware", "synthesizer", "generative", "fukuoka", "diy"]
---

## What it is

**MusicPixels** turns an [M5Stack Cardputer ADV](https://shop.m5stack.com) into a self-contained generative synthesizer. Music plays from the Cardputer's speaker; a transparent **M5 Unit Glass (U158)** OLED on the Grove port shows a different audio-reactive geometric scene for each genre; the LCD shows what's playing. It's the first project out of **CardputerADV Hacking Japan**, an IoTone hardware-hacking effort based in Fukuoka.

## Four genres, never the same twice

| Genre | Character | Glass scene |
|---|---|---|
| Ambient | drumless pads, sparse bells, heavy delay | breathing polygons + note ripples |
| Downtempo | ~78–92 BPM swung drums, dub bass, e-piano | beat-expanding rings + orbiters |
| Synthwave | ~100–112 BPM four-on-the-floor, arps | scrolling perspective grid + sun |
| Classical | rubato generative piano, Alberti bass | Lissajous curves from the melody |

Every entry is re-seeded on selection, so a genre never plays the same way twice.

## Under the hood

A 7-voice subtractive synth — polyBLEP oscillators, a TPT state-variable filter, ADSR, synthesized drums, a feedback delay, and a soft-clip master — renders in 256-sample blocks at 24 kHz on core 0 via M5Unified's I2S/DMA speaker. A dual-"performance" bus lets genre switches crossfade over a second. The whole thing runs on the microcontroller; the Unit Glass is optional (the app shows "GLASS NOT FOUND" and keeps playing without it).

## Status

Active. Build with PlatformIO (`pio run`) and launch from [M5Launcher](https://github.com/bmorcelli/M5Stick-Launcher) or flash over USB. Source on [github.com/IoTone](https://github.com/IoTone/CardputerADV_Hacking_Japan).
