---
title: "ESPIDFORTH"
date: 2026-08-14
draft: false
status: "active"
language: "C++"
license: "Apache-2.0"
github_url: "https://github.com/IoTone/ESPIDFORTH"
weight: 45
featured: false
hero_visual: "alt-3"
pill: "Forth on ESP32"
related_news: "/news/2026-08-14-espidforth/"
related_projects:
  - "project-magnet"
  - "poplog"
summary: "ESP32forth ported to ESP-IDF via PlatformIO — no Arduino layer — running on ESP32, S3, C3 and C6. Extracted from Project MAG*Net's Hive AI prototype so every consumer shares one versioned core."
tags: ["forth", "esp32", "esp-idf", "riscv", "iot", "embedded", "platformio"]
---

## What it is

A Forth interpreter running natively on **ESP-IDF** — built with PlatformIO, with no Arduino layer underneath it. Boot a board and you get a versioned banner with build info and memory stats, then an `ok>` prompt:

```
ok> : square dup * ;
ok> 7 square .
49
```

## Where it came from

ESPIDFORTH began as Phase 2 of the [Project MAG\*Net](/projects/project-magnet/) Hive AI prototype. In August 2026 we lifted it into a standalone repository with its full history preserved, so that MAG\*Net hive nodes and every other consumer share **one versioned core instead of drifting copies** — the usual fate of an interpreter living inside somebody's application tree.

## Targets

| Target | Status |
|---|---|
| ESP32-S3 | Builds — primary target (M5Stack Dial, 8MB PSRAM) |
| ESP32-C3 | Builds, tested on hardware — RISC-V, USB-serial-JTAG console |
| ESP32-C6 | Builds — RISC-V |
| ESP32 | Builds — classic Xtensa |

## What it implements

The core ANS Forth word set: arithmetic, the full stack vocabulary, comparison and logic, memory (`!` `@` `c!` `c@` `here` `allot`), defining words (`:` `;`, `variable`, `constant`), and control flow including `if`/`else`/`then`, `do`/`loop`/`+loop`, and the `begin`/`until`/`while`/`repeat` family.

Test suites are compiled in by default and stripped by a build flag — the C3 release build is **178 KB**, against 184 KB with tests included.

## Status

Active. Today the engine is a stub implementing that core word set; the full **ESP32forth v7.0.8.0** engine is preserved in `third_party/` and replaces the stub once its Arduino dependencies are fully stripped. Source on [github.com/IoTone/ESPIDFORTH](https://github.com/IoTone/ESPIDFORTH).
