---
title: "The Book of Math — the world's first XR math textbook"
date: 2026-08-26
draft: false
tags: ["release", "spectacles", "latex", "math", "matematex", "lensfest", "ar", "education"]
summary: "Eighty theorems across four chapters, rendered as real LaTeX on Snap Specs and paged through like a book. An IoTone, Inc. #Lensfest August 2026 drop — and the proof that Matematex, our LaTeX library for SPECS, is finished enough to build on."
source_url: "https://www.reddit.com/r/Spectacles/comments/1vzbmqv/lensfest_aug26_the_book_of_math_the_worlds_first/"
hero_image: "/images/news/book-of-math.jpg"
repo_url: "https://github.com/IoTone/Spectacles-Matematex"
video_url: "https://youtube.com/shorts/Sul6r2g20VY"
related_projects:
  - "spectacles-matematex"
  - "spectacles-polynode"
---

We dropped **The Book of Math** on [r/Spectacles](https://www.reddit.com/r/Spectacles/comments/1vzbmqv/lensfest_aug26_the_book_of_math_the_worlds_first/) as a #Lensfest August 2026 submission — *the world's first XR textbook for math, visualized, plus a LaTeX library for SPECS.* There's a [short demo video](https://youtube.com/shorts/Sul6r2g20VY) of the first edition, standing open in a room.

It is a book in the literal sense: **80 theorems across four chapters** — Geometry, Algebra, Calculus and Linear Algebra — that you page through with a pinch, with a page-turn sound and a running `3/80 Pythagorean Theorem` label. No scroll views, no tabs. Every formula is sourced from CC-licensed or public-domain material (ProofWiki, NIST's DLMF, OpenStax, Wikibooks, LibreTexts) and credited on the About page.

## The library underneath

The book is the demo. The deliverable is [**Spectacles-Matematex**](https://github.com/IoTone/Spectacles-Matematex), the LaTeX parser and renderer for Snap Spectacles we [started in July 2025](/news/2025-07-10-spectacles-matematex/) — and it has been finished the hard way.

LaTeX rendering on the web is built on DOM, canvas and SVG, none of which exist on Specs. So Matematex runs **KaTeX unmodified on top of SpaceDOM**, our off-screen DOM implementation, then walks the resulting tree into Lens Studio scene objects through **SpaceSVG** — both from the [Polynode](/projects/spectacles-polynode/) project. Two rejected alternatives and the comparison matrix that chose this one are written down in the design spec. Everything runs 100% on-device: no external service, no network call, no cloud LaTeX endpoint.

Getting there meant a per-formula visual defect catalog across all 80 formulas, a KaTeX font-metrics port, a proof grammar, and a long layout campaign. The integration guide names **six Lens Studio traps that each cost a day and none of which produce an error message** — that document alone is probably worth the repository.

## Small things that matter

The page-turn sound is an 11.3-second recording of a book being turned over and over; each turn plays a **random one-second window** of it, so no two consecutive pages sound identical. The same transient replayed twenty times while paging through a chapter is exactly what makes an interface sound synthetic.

The sample lens is `Matematex/` — open it in Lens Studio, enable the Phase 6 scene object, and it validates all 80 formulas on startup. Source, design docs, and the integration guide on [github.com/IoTone/Spectacles-Matematex](https://github.com/IoTone/Spectacles-Matematex).
