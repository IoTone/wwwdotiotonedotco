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

## Status

Active. New protocol surfaces land roughly quarterly. Documentation site at [projectmagnet.github.io](https://github.com/IoTone/projectmagnet.github.io).
