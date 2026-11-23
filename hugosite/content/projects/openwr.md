---
title: "OpenWR"
date: 2024-03-31
draft: false
status: "active"
language: "C++"
license: "MIT"
github_url: "https://github.com/IoTone/OpenWR"
weight: 55
featured: false
hero_visual: "alt-3"
pill: "Open hardware"
related_news: "/news/2024-03-31-openwr/"
summary: "An open hardware standard for wearables that work together with no account, no cloud and no company able to switch them off. Now home to NFC taps in XR, a wearable camera remote, an e-paper backstage-pass reader and an open XR display design."
tags: ["hardware", "wearable", "iot", "openhardware", "snap-spectacles", "nfc", "e-paper", "xr"]
---

## What it is

OpenWR (OpenWear) is an open hardware standard for wearable IoT devices. The idea is that things you wear should link up and work together, the way clothing does, and that you should own them outright: no app login unless you want one, no third-party cloud needed to get started, and no company able to cut off your devices. Hardware designs and their software are published together.

## What is being built

Active development is on the [`dev` branch](https://github.com/IoTone/OpenWR/tree/dev):

- **NFCTapInXR** — a Snap Spectacles lens that plays a scene in the air when you tap an NFC tag on a small ESP32 reader. [Watch the video](https://youtu.be/uXBH_5CcVdo).
- **LightScopeXR** — a remote for a Sony α7R III on Spectacles, with the Scout second camera and the ReelHub shot hub.
- **SubverseReader** — a wearable e-paper reader the size of a backstage pass, targeting $50 or less, in sixteen variants with parts lists and printable enclosures.
- **Hiroglass** — an open design for XR displays that attach to existing glasses, goggles and helmets. Research and concepts so far.
- **Switchback** and **SwitchbackXR** — the OpenWR phone app and its Spectacles counterpart, for the goggl1 ski-goggle display.

Read more in [OpenWR comes back to life](/news/2026-11-23-openwr-nfc-tap-in/).

## Status

Active. The earlier HeadsOut display and headlight prototypes remain on the main branch.
