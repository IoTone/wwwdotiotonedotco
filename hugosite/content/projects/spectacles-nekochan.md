---
title: "Spectacles NekoChan"
date: 2026-07-09
draft: false
status: "active"
language: "TypeScript"
license: "MIT"
github_url: "https://github.com/IoTone/Spectacles-NekoChan"
weight: 17
featured: false
hero_visual: "alt-1"
pill: "AR · Offline JP"
related_news: "/news/2026-07-09-spectacles-nekochan/"
related_projects:
  - "spectacles-polynode"
  - "snap-spectacles-ik-samples"
summary: "A fully on-device Snap Spectacles lens: a 3D cat that shares facts — in Japanese — about native breeds and Japan's cat islands. No internet, no experimental APIs."
tags: ["spectacles", "ar", "offline", "japanese", "localization", "sample"]
---

## What it is

**NekoChan** (ネコちゃん) is a Snap Spectacles lens where a 3D cat sits in your space; tap it and it shares a piece of trivia — in Japanese — about **native Japanese cat breeds** (ジャパニーズボブテイル, 三毛猫), folklore (招き猫, 猫又), and Japan's famous **cat islands** (猫島 — 田代島, 青島, 相島).

Built on Snap's Fetch demo, it's rebuilt as a reference for two things that are surprisingly hard on AR glasses: **running fully offline**, and **rendering Japanese correctly**.

## Why it's a reference build

- **Fully local, no internet.** Every fact is bundled in a TypeScript array; nothing is fetched over the network, and the Internet capability is never requested. It works with the glasses in airplane mode.
- **Japanese renders correctly.** A *subsetted* Noto Sans JP font (~305 KB instead of several MB) ships in the lens, containing only the glyphs the app actually uses — so every kanji and kana renders instead of showing tofu (□) boxes.
- **No experimental APIs.** Only stable modules — Text, AnimationPlayer, the Spectacles Interaction Kit, LSTween, Audio — so it keeps working across Lens Studio updates.

The repo includes the tooling (`subset_font.py`, `generate_audio.py`) to regenerate the font subset and optional offline narration whenever you edit the content, so localizing to new text — or a new language — is a documented, repeatable step.

## Status

Active. MIT-licensed; source on [github.com/IoTone](https://github.com/IoTone/Spectacles-NekoChan).
