---
title: "Project MAG*Net"
date: 2024-01-20
draft: false
status: "active"
language: "C++"
license: "MIT"
github_url: "https://github.com/IoTone/ProjectMagNET"
weight: 10
featured: true
hero_visual: "alt-1"
pill: "IoT runtime"
related_news: "/news/2024-01-20-project-magnet/"
related_projects:
  - "espidforth"
summary: "Distributed IoT data sync &amp; control across Matter, Zigbee, Thread, HomeKit, BLE, and Wi-Fi. ESP32 firmware + C++ runtime."
tags: ["iot", "matter", "zigbee", "thread", "homekit", "esp32", "ble", "mqtt", "wifi"]
---

## What it is

Project MAG\*Net is the spiritual successor to IoToneKit. It's an IoT data sync and control app + a distributed server, designed to span Matter, Zigbee, Thread, HomeKit, BLE, and Wi-Fi without locking developers into a single platform.

The big tech vendors want lock-in; MAG\*Net is the OSS counterweight.

## What it ships

- **Runtime** — C++ core that ingests data from IoT devices over multiple protocols and exposes a unified MQTT interface.
- **Firmware reference** — ESP32 + Arduino tooling for the device side.
- **Cross-protocol sync** — translate between protocol stacks without hardcoding a particular vendor SDK.
- **WebXR of Things** — browser-first spatial UI reference design that drives Matter/Zigbee/Thread/BLE/Wi-Fi fleets over the MAG\*Net stack. Submitted as a poster to [MeaningfulXR 2026](/news/2026-05-22-webxr-of-things-meaningfulxr-2026/) (MXR26) by IoTone Japan, source on the [`dev/reference-designs/webxrofthings`](https://github.com/IoTone/ProjectMagNET/tree/dev/reference-designs/webxrofthings) branch.

## Status

Active. New protocol surfaces land roughly quarterly. Documentation site at [projectmagnet.github.io](https://github.com/IoTone/projectmagnet.github.io).
