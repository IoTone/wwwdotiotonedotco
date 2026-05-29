---
title: "MIDI Bleep Blop"
date: 2026-05-28
draft: false
status: "active"
language: "TypeScript"
license: "MIT"
github_url: "https://github.com/IoTone/MIDIBleepBlop"
weight: 16
featured: true
hero_visual: "alt-3"
pill: "AR · MIDI"
related_news: "/news/2026-05-28-midi-bleep-blop/"
related_projects:
  - "spectacles-skywriter-ble"
  - "spectacles-polynode"
summary: "A MIDI library and bridge that turns a Snap Spectacles lens into a controller for real hardware synths. #Lensfest May 2026 OSS, with a Tester Lens."
tags: ["spectacles", "midi", "music", "websocket", "ar", "korg-volca"]
---

## What it is

A MIDI library that lets you generate MIDI notes from different platforms — including a Snap Spectacles '24 lens — and play them on real synths. Pure TypeScript, MIT-licensed, with device-catalog data under CC-BY-SA-4.0.

Released as a #Lensfest May 2026 OSS submission, complete with a **Tester Lens** so you can try the whole chain on your own Spectacles before touching the code. There's a [demo video](https://youtu.be/FY7x7KbuUoQ) of a live performance.

## How it works

Spectacles can't speak MIDI to a synth directly, so MIDI Bleep Blop routes the data off-device:

- A lens generates note and control-change events.
- Those ship over a **WebSocket bridge** to a companion process on your computer.
- The bridge hands them to the OS MIDI subsystem — CoreMIDI (macOS), ALSA (Linux), or WinMM (Windows).
- From there it's just MIDI — any synth, soft or hard, picks it up.

## What it ships

- **Pure-TS MIDI library** — note and CC helpers with state tracking, no native dependencies.
- **WebSocket transports** for both Node and Lens Studio.
- **Device catalogs** for hardware synths, starting with the KORG Volca line.
- **Groove generators** — built-in acid, house, and trance patterns.
- **Lens Studio components** — a piano keyboard and CC parameter controls, plus per-channel output routing.
- **A Tester Lens** for a no-code first run.

## Why

Music performance is a natural fit for spatial computing — hands free, infinite surface, and a latency budget forgiving enough to survive a WebSocket hop. MIDI Bleep Blop is the reference plumbing for turning a Spectacles lens into an instrument.

## Status

Active. macOS is the primary bridge target; Linux and Windows are supported. [Release thread on r/Spectacles](https://www.reddit.com/r/Spectacles/comments/1tqsdnw/lensdrop_midi_bleep_blop_a_midi_library_and/).
