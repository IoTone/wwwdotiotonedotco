---
title: "ESPIDFORTH — Forth on bare ESP-IDF, pulled out of Project MAG*Net"
date: 2026-08-14
draft: false
tags: ["release", "forth", "esp32", "esp-idf", "riscv", "iot", "embedded", "magnet"]
summary: "ESP32forth ported to ESP-IDF via PlatformIO — no Arduino layer — running on ESP32, S3, C3 and C6. Extracted from Project MAG*Net's Hive AI prototype into a standalone repo so every consumer shares one versioned core."
source_url: "https://github.com/IoTone/ESPIDFORTH"
repo_url: "https://github.com/IoTone/ESPIDFORTH"
related_projects:
  - "espidforth"
  - "project-magnet"
---

[**ESPIDFORTH**](https://github.com/IoTone/ESPIDFORTH) is ESP32forth ported to **ESP-IDF via PlatformIO** — a Forth interpreter running natively on the IDF, with no Arduino layer underneath it.

It began as Phase 2 of the [Project MAG\*Net](/projects/project-magnet/) Hive AI prototype. In August 2026 we lifted it out into a standalone repository with its full history preserved, so that MAG\*Net hive nodes and every other consumer share **one versioned core instead of drifting copies** — the usual fate of an interpreter that lives inside somebody's application tree.

## Targets

| Target | Status |
|---|---|
| ESP32-S3 | Builds — primary target (M5Stack Dial, 8MB PSRAM) |
| ESP32-C3 | Builds, tested on hardware — RISC-V, USB-serial-JTAG console |
| ESP32-C6 | Builds — RISC-V |
| ESP32 | Builds — classic Xtensa |

## What you get

Boot the board and you get a versioned banner with build info and memory stats, then an `ok>` prompt — the core ANS Forth word set, live on the device:

```
ok> : square dup * ;
ok> 7 square .
49
```

Arithmetic, the full stack vocabulary, comparison and logic, memory (`!` `@` `c!` `c@` `here` `allot`), defining words, and control flow including `do`/`+loop` and the `begin`/`while`/`repeat` family. Test suites are compiled in by default and stripped by a build flag: the release build for the C3 is **178 KB**, against 184 KB with tests.

Today the engine is a stub implementing that core word set. The full **ESP32forth v7.0.8.0** engine is preserved in `third_party/` and replaces the stub once its Arduino dependencies are fully stripped.

Apache-2.0. Source on [github.com/IoTone/ESPIDFORTH](https://github.com/IoTone/ESPIDFORTH).
