---
title: "SPECS CLAD Starter — agentic Lens development, from zero"
date: 2026-09-29
draft: false
tags: ["release", "spectacles", "specs", "lens-studio", "clad", "ai-agents", "claude", "codex", "cursor"]
summary: "A starter project for building SPECS Lenses with coding agents — Claude, Codex, or Cursor — driving Lens Studio 5.2x over MCP. Setup steps, the gotchas per agent, and the prompting discipline that separates a ten-minute toy from a shippable Lens."
source_url: "https://github.com/IoTone/SPECS_CLADStarter"
hero_image: "/images/news/specs-clad-starter.jpg"
video_url: "https://youtu.be/s8ZL-fFElE4"
repo_url: "https://github.com/IoTone/SPECS_CLADStarter"
related_projects:
  - "megauikit-specs"
  - "spectacles-skywriter-ble"
---

[**SPECS_CLADStarter**](https://github.com/IoTone/SPECS_CLADStarter) is a starter project for quick onboarding into **agentic Lens development** — CLAD workflows where a coding agent (Claude, Codex, or Cursor) drives Lens Studio 5.2x over an MCP connection and builds your SPECS Lens with you.

After a season of shipping Lenses this way — [SkyWriterBLE](/news/2026-04-26-skywriterble-wins-3rd-place-lensfest-april-2026/), [NekoChan](/news/2026-07-09-spectacles-nekochan/), [MegaUIKit](/news/2026-08-16-megauikit-specs/) — this repo is the on-ramp we wished existed on day one. There's a [demo video](https://youtu.be/s8ZL-fFElE4) of the workflow in action.

## What's in it

- **Setup, in order**: Lens Studio 5.24+, your agent of choice, the CLAD plugins, the MCP connection, and the separate *specs* account (it's additional to your Snapchat account) — with the known gotchas per agent called out, mostly around account and login types.
- **Prompting discipline.** The magic is in constraining the request. "Design a pool" can go anywhere; "Design a SPECS Lens with a pool full of plastic balls with real physics you can push around with your hands — make it a game to empty the pool" goes somewhere specific. The README grades examples by time-to-result, from a ten-minute Codex one-shot to a thirty-minute castle-defense tabletop game.
- **SPECS 24 backporting.** Not officially supported, but CLAD can backport a design to Lens Studio 5.15.4 for the 2024 hardware, and the README points at how.

Clone it or start from Snap's Base Template — either way, the point is to be building within the hour. Source on [github.com/IoTone/SPECS_CLADStarter](https://github.com/IoTone/SPECS_CLADStarter).
