---
title: "Spectacles-Matematex"
date: 2025-07-10
draft: false
status: "active"
language: "TypeScript"
license: "MIT"
github_url: "https://github.com/IoTone/Spectacles-Matematex"
weight: 20
featured: true
hero_visual: "alt-3"
pill: "Math in AR"
related_news: "/news/2026-08-26-book-of-math/"
related_projects:
  - "spectacles-polynode"
summary: "A LaTeX parser and renderer for Snap Spectacles — KaTeX running unmodified on an off-screen DOM, walked into Lens Studio scene objects. Shipped as The Book of Math: 80 theorems across four chapters, entirely on-device."
tags: ["spectacles", "ar", "latex", "math", "katex", "education"]
---

## What it is

Matematex parses and renders **LaTeX math notation on Snap Spectacles**, spatially. It is a reusable TypeScript library for Lens Studio, plus the lens that proves it works: [**The Book of Math**](/news/2026-08-26-book-of-math/), an #Lensfest August 2026 drop of 80 theorems across four chapters — Geometry, Algebra, Calculus and Linear Algebra — paged through with a pinch.

## How it works

LaTeX rendering on the web is built on DOM, canvas and SVG. None of those exist on Specs. Rather than reimplement a typesetter, Matematex runs **KaTeX unmodified on top of SpaceDOM** — an off-screen DOM implementation — then walks the resulting tree into Lens Studio scene objects through **SpaceSVG**. Both come from the [Polynode](/projects/spectacles-polynode/) project, and Matematex is the use case that drove Polynode in the first place.

That approach ("Approach A") was chosen over two alternatives that are written up, with the comparison matrix, in the design spec. Everything runs **100% on-device**: no external service, no network call, no cloud LaTeX endpoint.

## What shipped

- The renderer, validated against a per-formula **visual defect catalog covering all 80 formulas**.
- A KaTeX font-metrics port, so glyph positioning matches what KaTeX intends.
- A **proof grammar** for rendering theorems with their proofs.
- A search index, chapter navigation, and a Spectacles UIKit pass over the book's UI.
- An [integration guide](https://github.com/IoTone/Spectacles-Matematex/blob/main/MATEMATEX.md) naming the **six Lens Studio traps that each cost a day and none of which produce an error message** — arguably the most valuable file in the repository.

All formula content is sourced from CC-licensed or public-domain material (ProofWiki, NIST's DLMF, OpenStax, Wikibooks, LibreTexts) and credited on the lens's About page.

## Status

Active and shipping. The sample lens is `Matematex/` — open it in Lens Studio, enable the Phase 6 scene object, and it validates all 80 formulas on startup. Next up: shared viewing of diagrams, web publishing of content, and spatial content libraries.
