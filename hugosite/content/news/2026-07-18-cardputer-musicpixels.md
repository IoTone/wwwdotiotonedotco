---
title: "MusicPixels — a generative synth on the M5 Cardputer ADV + Unit Glass"
date: 2026-07-18
draft: false
tags: ["release", "hardware", "m5stack", "cardputer", "synthesizer", "fukuoka", "generative"]
summary: "CardputerADV Hacking Japan opens with MusicPixels: a self-contained generative synthesizer for the M5Stack Cardputer ADV, with audio-reactive geometry on a transparent M5 Unit Glass OLED."
source_url: "https://github.com/IoTone/CardputerADV_Hacking_Japan"
repo_url: "https://github.com/IoTone/CardputerADV_Hacking_Japan"
related_projects:
  - "cardputer-musicpixels"
---

We kicked off **CardputerADV Hacking Japan** — an IoTone hardware-hacking effort out of Fukuoka — with its first project, [MusicPixels](https://github.com/IoTone/CardputerADV_Hacking_Japan).

MusicPixels turns an [M5Stack Cardputer ADV](https://shop.m5stack.com) into a stand-alone generative synthesizer. Music plays from the built-in speaker; a transparent **M5 Unit Glass (U158)** OLED on the Grove port renders a different audio-reactive geometric scene per genre; the LCD shows what's playing.

## Four genres, re-seeded every time

Ambient (breathing polygons + note ripples), Downtempo (beat-expanding rings), Synthwave (a scrolling perspective grid + sun), and Classical (Lissajous curves drawn from the melody). Each is re-randomized from a fresh seed on selection, so it never plays the same way twice, and genre switches crossfade over a second.

## What's inside

A 7-voice subtractive synth — polyBLEP oscillators, a TPT state-variable filter, ADSR, synthesized drums, feedback delay, and a soft-clip master — renders in 256-sample blocks at 24 kHz on core 0 via M5Unified's I2S/DMA speaker. It runs entirely on the microcontroller; the Unit Glass is optional (no Glass, no problem — the music and LCD keep going).

Build with PlatformIO and launch from [M5Launcher](https://github.com/bmorcelli/M5Stick-Launcher), or flash over USB. Source on [github.com/IoTone](https://github.com/IoTone/CardputerADV_Hacking_Japan).
