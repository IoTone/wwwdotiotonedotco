---
title: "MIDI Bleep Blop — perform on live synths from a Spectacles lens"
date: 2026-05-28
draft: false
tags: ["release", "spectacles", "midi", "music", "websocket", "lensfest", "ar"]
summary: "A MIDI library and bridge so you can perform on live musical instruments from a Snap Spectacles lens — now with a Tester Lens you can try yourself. An IoTone, Inc. #Lensfest May 2026 OSS drop."
source_url: "https://www.reddit.com/r/Spectacles/comments/1tqsdnw/lensdrop_midi_bleep_blop_a_midi_library_and/"
repo_url: "https://github.com/IoTone/MIDIBleepBlop"
video_url: "https://youtu.be/FY7x7KbuUoQ"
related_projects:
  - "midi-bleep-blop"
---

We dropped [MIDI Bleep Blop](https://www.reddit.com/r/Spectacles/comments/1tqsdnw/lensdrop_midi_bleep_blop_a_midi_library_and/) on [r/Spectacles](https://www.reddit.com/r/Spectacles/) as a #Lensfest May 2026 OSS submission — *a MIDI library and bridge so you can perform on live musical instruments, with a Tester Lens you can try yourself.*

It's a MIDI library that lets you generate MIDI notes from different platforms — including a Snap Spectacles '24 lens — and play them on real synths. MIT-licensed, written in TypeScript. There's a [demo video](https://youtu.be/FY7x7KbuUoQ) of a live performance: notes triggered from the glasses, played out through hardware.

## How it works

Spectacles can't speak MIDI to your synth directly, so MIDI Bleep Blop routes the data off-device. A lens generates the note and control-change events, ships them over a **WebSocket bridge** to a companion process on your computer, and that process hands them to the OS MIDI subsystem — CoreMIDI on macOS, ALSA on Linux, or WinMM on Windows. From there it's just MIDI: any synth, soft or hard, picks it up.

## What it ships

- **Pure-TS MIDI library** — note and control-change helpers with state tracking, no native dependencies.
- **WebSocket transports** for both Node and Lens Studio.
- **Device catalogs** for hardware synths, starting with the KORG Volca line (catalog data under CC-BY-SA-4.0).
- **Groove generators** — built-in acid, house, and trance patterns.
- **Lens Studio components** — a piano keyboard and CC parameter controls, plus per-channel output routing.
- **A Tester Lens** — so you can try the whole chain on your own Spectacles before touching the code.

## Why

Spatial computing keeps looking for inputs that aren't just taps and gaze. Music performance is a natural fit — your hands are free, the surface is infinite, and the latency budget for triggering a synth survives a WebSocket hop. MIDI Bleep Blop is the reference plumbing for anyone who wants to turn a Spectacles lens into an instrument.

Release thread on [r/Spectacles](https://www.reddit.com/r/Spectacles/comments/1tqsdnw/lensdrop_midi_bleep_blop_a_midi_library_and/) · source on [github.com/IoTone](https://github.com/IoTone/MIDIBleepBlop).
