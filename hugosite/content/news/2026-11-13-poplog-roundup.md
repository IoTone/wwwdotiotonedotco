---
title: "Poplog round-up — a hang hunted down, notebooks in one command, and a new book chapter"
date: 2026-11-13
draft: false
tags: ["update", "poplog", "pop-11", "jupyter", "jevracket", "laya", "project-magnet", "ota"]
summary: "A month of smaller news from the IoTone repositories: Poplog's intermittent test-suite hang turned out to be two separate bugs and both are fixed, Pop-11 notebooks now open with one command, and the Poplog book gains a ninth chapter on typed judgment. Plus briefs from jevracket, which now works against self-hosted Laya, and Project Mag*NET, whose nodes take firmware over the air."
source_url: "https://github.com/IoTone/poplog"
hero_image: "/images/news/poplog.png"
repo_url: "https://github.com/IoTone/poplog"
related_projects:
  - "poplog"
  - "project-magnet"
---

Not everything earns its own post. Here is what else moved in the public IoTone repositories over the past month.

## Poplog

Our [Poplog](https://github.com/IoTone/poplog) port for Apple silicon, Raspberry Pi 5 and RISC-V had a busy week after the October release.

**The hang is solved.** Moving the release gate to hosted CI meant all 16 library suites ran on every platform for the first time, and about a quarter of the test legs started wedging. The investigation went through three explanations that each fit every symptom and were each ruled out by a measurement. The answer was two unrelated bugs:

- On x86_64 Linux, `read_pipe` treated a pipe at end of file as still alive and spun a full core for ever.
- On macOS and aarch64, a child process could die before Poplog had listed it, so the signal announcing its death was lost and the parent waited for good.

A third real bug turned up along the way and was fixed with a regression test. The [write-up](https://github.com/IoTone/poplog/blob/master/docs/bugs/sigchld-coalesce-lost-child-status.md) keeps every dead hypothesis and what killed it, which is the useful part for anyone debugging process handling on these platforms.

**Releases from one tag.** `skill-2026.10.1` shipped on October 17. A release is now a single tag instead of a build on four machines, and each tarball is installed from scratch into an unrelated path before it is published.

**Notebooks in one command.** `tools/jupyter/lab.sh` sets up a locked environment, registers the Pop-11 kernel and opens the example notebooks in JupyterLab. The earlier installer registered a working kernel and then recommended two commands it had not installed.

**Chapter 9 of the book.** *The fleet takes counsel* has the robot army's command post ask an adviser typed questions and get typed answers back: a pick from fixed options, a probability, or a score. It runs against either hosted Jev or a local Laya model with no change at the call site, and every transcript in the chapter came from a live run.

## jevracket

[jevracket](https://github.com/IoTone/jevracket), our Racket client for TypeSafe's System One API, now also works against **Laya**, a self-hosted engine that accepts requests in the same format, including its Apple MLX port. The README documents the five differences to know about, the main one being to turn request compression off. One caution from our own testing: Laya's answers differ from Jev's, so confidence thresholds tuned on one need re-tuning for the other.

## Project Mag\*NET

The NanoC6 nodes in [Project Mag\*NET](https://github.com/IoTone/ProjectMagNET) gained **over-the-air firmware builds** in mid-October. A node now reports which build it is running, and the app shows it on the node's screen, so you can tell what is installed without plugging in a cable. The same batch of work added a hive role for audio capture.

## Elsewhere

Three bigger items have their own posts today: [Spicemine](/news/2026-11-13-spicemine/), our collaboration with IoTone Japan; [langpop](/news/2026-11-13-langpop/), a language tutor in Pop-11; and the [Telemachus 0.12.0](/news/2026-11-13-telemachus-0-12/) security release.
