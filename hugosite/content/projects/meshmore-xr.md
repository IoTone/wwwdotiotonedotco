---
title: "Meshmore XR"
date: 2026-09-08
draft: false
status: "active"
language: "Kotlin"
license: "MIT (X11)"
github_url: "https://github.com/IoTone/meshmore-sns/tree/main/meshmore-xr"
product_url: "https://meshmore-xr-www.pages.dev/"
weight: 11
featured: true
hero_visual: "alt-5"
pill: "Mesh in XR"
related_news: "/news/2026-09-08-meshmore-xr/"
related_projects:
  - "offlinesns"
summary: "The first mesh-networking application built for XR glasses. Every node your MeshCore LoRa radio can hear, standing around you at its true compass bearing — no phone, no server, no account, no internet."
tags: ["meshcore", "lora", "xr", "android-xr", "offline", "japan", "mesh", "open-source"]
---

## What it is

**Meshmore XR** turns a [MeshCore](https://meshcore.co.uk/) LoRa companion radio and a pair of optical see-through glasses into a spatial view of your mesh. No phone in your hand, no map on a screen — the nodes stand in the room around you, at their true bearings, at a glance.

## Why

MeshCore radios already form resilient, encrypted, many-hop LoRa networks that work where nothing else does — trails, festivals, disasters, open water. But every client until now rendered that living network the same way: a list and a map, in a rectangle, in your hand.

A mesh is not a list. Every node is *somewhere* — over that ridge, three streets east, behind you. Meshmore XR makes the network's real geography the interface. You do not scroll to a repeater; you look toward it.

To our knowledge it is the first mesh-networking application built for XR glasses, and the first XR client for MeshCore. Glasses on your face, a radio in your pocket: a complete, infrastructure-free communications system, heads up and hands free in exactly the situations a mesh exists for.

## What it does

- **The Horizon** — every node your radio can hear, placed by real compass bearing and range. Live nodes hold the ring; a quiet mesh looks quiet.
- **Nine themes, three postures** — a room-scale field, an active mode that moves with you on a hike or a ride, and a tabletop diorama that anchors to a real desk and remembers it.
- **Find anyone** — search by name or key, star your friends' nodes, tag the ones from that trip.
- **Messages, hands-free** — threads read aloud per channel, replies by dictation or one-pinch canned responses, a wrist reel for triage.
- **Channels by voice** — create a channel with a rolled two-word name and share it by saying it out loud, with honest guidance about what a spoken key can and cannot keep private.
- **日本語 throughout**, at kanji-legible sizes — a launch language, not a translation pass.

## What it needs

Android XR glasses (built and tested on the **XREAL Aura**) and a MeshCore LoRa companion radio over Bluetooth. Nothing else: no account, no server, **no internet permission**.

## Source

Meshmore XR is **open source under the MIT (X11) License** — use it, modify it, ship it, commercially or otherwise, as long as the copyright notice travels with it. The code lives in the [meshmore-sns monorepo](https://github.com/IoTone/meshmore-sns/tree/main/meshmore-xr), alongside the phone client it shares a mesh with.

## Status

Active, v0.3.0, in development against a live **350-node mesh** with a Japan launch in preparation. The spatial member of the [Offline SNS](/projects/offlinesns/) family — [Meshmore SNS](https://github.com/IoTone/meshmore-sns) carries the same mesh on phones, and the device guide covers the radios that run it. Follow the [product page](https://meshmore-xr-www.pages.dev/) for the release.
