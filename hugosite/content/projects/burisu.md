---
title: "Burisu (ブライス)"
date: 2026-07-23
draft: false
status: "active"
language: "Rust"
license: "MIT"
github_url: "https://github.com/IoTone/burisu"
weight: 12
featured: true
hero_visual: "alt-5"
pill: "WebGPU · WASM"
related_news: "/news/2026-07-23-burisu/"
related_projects:
  - "gsplats-to-webxr"
  - "spectacles-polynode"
summary: "A browser-native remake of the classic KPT Bryce 3D landscape generator — Rust compiled to WASM, rendered with WebGPU, tuned to run on a 4GB Raspberry Pi 5."
tags: ["rust", "wasm", "webgpu", "3d", "terrain", "retro", "creative-tools"]
---

## What it is

**Burisu** (ブライス) reimagines [KPT Bryce](https://en.wikipedia.org/wiki/Bryce_(software)) — the 1990s fractal-landscape program that a generation of artists used to render alien terrain and impossible skies — as a modern, fully client-side web app. The engine is written in **Rust**, compiled to **WASM**, and renders through **WebGPU** in the browser. No install, no cloud, no Node runtime required to view it.

## How it works

A Rust engine built on [`wgpu`](https://wgpu.rs) handles the scene model, procedural terrain generation, and a progressive ray-traced renderer. A TypeScript/Svelte UI shell recreates the spirit of the original Bryce workspace — tool palettes, a preset rail, a nano preview, and full-screen "labs." Everything runs locally and works offline.

The project also sketches **"Muse,"** a REPL-first scene DSL (Poplog-inspired) with optional text/STT intent parsing and tiered LLM backends for driving the UI by description.

## The constraint that shapes it

The **Raspberry Pi 5 (4GB)** is the reference target, and it *gates releases*. If a build doesn't hit an acceptable frame rate on a Pi 5's V3D GPU in browser-compat mode, it doesn't ship. That constraint drove a whole [catalog of WebGPU platform notes](https://github.com/IoTone/burisu/blob/main/docs/WEBGPU-PLATFORM-NOTES.md) — x86-vs-Pi driver bugs, readback/presentation quirks, and testing traps — that are useful to anyone shipping WebGPU to low-end hardware.

## Status

Active, early. Milestone M0 ("hello terrain") renders a slowly orbiting fractal landscape; the roadmap runs through M6 plus an AI milestone. Requires a WebGPU-enabled browser. Source and design docs (FSD, UX plan, implementation roadmap) are on [github.com/IoTone](https://github.com/IoTone/burisu).
