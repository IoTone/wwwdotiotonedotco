---
title: "Meshmore XR — your LoRa mesh, standing in the room around you"
date: 2026-09-08
draft: false
tags: ["announcement", "meshmore", "xr", "lora", "meshcore", "android-xr", "offline", "japan", "open-source"]
summary: "The first mesh-networking application built for XR glasses: every node your MeshCore radio can hear, placed around you at its true compass bearing. No phone, no server, no account, no internet anywhere in the loop. MIT-licensed, with a Japan launch in preparation."
source_url: "https://meshmore-xr-www.pages.dev/"
repo_url: "https://github.com/IoTone/meshmore-sns/tree/main/meshmore-xr"
hero_image: "/images/news/meshmore-xr.jpg"
product_url: "https://meshmore-xr-www.pages.dev/"
related_projects:
  - "meshmore-xr"
  - "offlinesns"
---

We put up the page for [**Meshmore XR**](https://meshmore-xr-www.pages.dev/) — *the mesh, around you.* It is what a mesh network looks like when you stop squeezing it into a phone.

[MeshCore](https://meshcore.co.uk/) radios already form resilient, encrypted, many-hop LoRa networks that work where nothing else does — trails, festivals, disasters, open water. But every client until now has rendered that living network the same way: a list and a map, in a rectangle, in your hand.

A mesh is not a list. Every node is *somewhere* — over that ridge, three streets east, behind you. Meshmore XR takes that seriously: **the network's real geography becomes the interface.** Nodes stand in the room and on the horizon at their true bearings. You do not scroll to a repeater; you look toward it.

To our knowledge this is the **first mesh-networking application built for XR glasses**, and certainly the first XR client for MeshCore. Glasses on your face, a radio in your pocket: a complete, infrastructure-free communications system — heads up and hands free in exactly the situations a mesh exists for.

## What it does

- **The Horizon.** Every node your radio can hear, placed around you by real compass bearing and range. Live nodes hold the ring; a quiet mesh looks quiet.
- **Nine themes, three postures.** A room-scale field, an active mode that moves with you on a hike or a ride, and a tabletop diorama that anchors to a real desk and remembers it.
- **Find anyone.** Search by name or key, star your friends' nodes, tag the ones from that trip — the ways people actually remember radios.
- **Messages, hands-free.** Threads read aloud per channel if you ask, replies by dictation or one-pinch canned responses, a wrist reel for triage.
- **Channels by voice.** Create a channel with a rolled two-word name and share it by saying it out loud — with clear guidance about what a spoken key can and cannot keep private.
- **Speaks Japanese.** 日本語 throughout, at kanji-legible sizes. Not a translation pass — a launch language.

## What it needs

Android XR glasses (built and tested on the **XREAL Aura**) and a **MeshCore** LoRa companion radio over Bluetooth. Nothing else: **no account, no server, no internet permission.** The privacy policy is short because there is nothing to disclose.

## Open source

Meshmore XR is released under the **MIT (X11) License** — use it, modify it, ship it, commercially or otherwise, as long as the copyright notice travels with it. The code lives in the [meshmore-sns monorepo](https://github.com/IoTone/meshmore-sns/tree/main/meshmore-xr). The source is developed by **IoTone, Inc.**; the application is released by **IoTone Japan**, which handles the app's release and support.

## Part of Offline SNS

Meshmore XR is the spatial member of a family. [**Meshmore SNS**](https://github.com/IoTone/meshmore-sns) carries the same mesh on phones, the device guide covers the radios that run it, and the [Offline SNS project](/projects/offlinesns/) is the why behind all of it — off-grid communications for a country where cellular and Wi-Fi go down.

In active development against a live **350-node mesh**, v0.3.0, with a Japan launch by IoTone Japan in preparation. Follow [the page](https://meshmore-xr-www.pages.dev/) for the release.
