---
title: "NekoChan — a fully-offline Japanese cat lens for Spectacles"
date: 2026-07-09
draft: false
tags: ["release", "spectacles", "ar", "offline", "japanese", "localization"]
summary: "Spectacles-NekoChan is a Snap Spectacles lens where a 3D cat shares facts — in Japanese — about native breeds and Japan's cat islands, running entirely on-device with no internet and no experimental APIs."
source_url: "https://github.com/IoTone/Spectacles-NekoChan"
repo_url: "https://github.com/IoTone/Spectacles-NekoChan"
related_projects:
  - "spectacles-nekochan"
---

We released [Spectacles-NekoChan](https://github.com/IoTone/Spectacles-NekoChan) (ネコちゃん) — a Snap Spectacles lens where a 3D cat sits in your space and, when you tap it, shares a piece of trivia *in Japanese* about native Japanese breeds (ジャパニーズボブテイル, 三毛猫), folklore (招き猫, 猫又), and Japan's cat islands (猫島 — 田代島, 青島, 相島).

It's cute on the surface, but it's really a reference build for two things that are quietly hard on AR glasses:

- **Running fully offline.** Every fact is bundled with the lens; nothing is fetched over the network, and the Internet capability is never requested. It works in airplane mode.
- **Rendering Japanese correctly.** A *subsetted* Noto Sans JP font (~305 KB, only the glyphs the app uses) ships inside the lens, so every kanji and kana renders instead of showing tofu (□) boxes — a common failure when non-Latin text meets a size-constrained AR runtime.

It also sticks to **stable APIs only** (Text, AnimationPlayer, the Spectacles Interaction Kit, LSTween, Audio), and includes the tooling to regenerate the font subset and offline narration when you edit the content — so relocalizing it is a documented, repeatable step. Source on [github.com/IoTone](https://github.com/IoTone/Spectacles-NekoChan).
