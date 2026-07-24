---
title: "Poplog"
date: 2026-07-24
draft: false
status: "active"
language: "Pop-11 · C"
license: "MIT-style (free Poplog)"
github_url: "https://github.com/IoTone/poplog"
weight: 8
featured: true
hero_visual: "gradient"
pill: "AI heritage revived"
related_news: "/news/2026-07-24-poplog/"
related_projects:
  - "burisu"
summary: "We brought Poplog — the classic multi-language AI development environment (Pop-11, Prolog, Common Lisp, Standard ML) — natively onto Apple Silicon, Raspberry Pi 5, and RISC-V. Then we added a fifth language, a real ELIZA, native graphics, and a full benchmark suite."
tags: ["poplog", "pop-11", "prolog", "common-lisp", "standard-ml", "forth", "eliza", "ai-history", "riscv", "apple-silicon", "raspberry-pi", "porting", "benchmarks", "claude"]
---

## What it is

[Poplog](https://en.wikipedia.org/wiki/Poplog) is one of the great artifacts of AI history — a multi-language software development environment from the University of Sussex, built around fast **incremental compilers** for four interactive languages that share one virtual machine and one saved image, and interoperate freely:

- **Pop-11** — the core language, with the Objectclass OO extension (a CLOS-for-Pop),
- **Prolog** — standard Edinburgh syntax,
- **Common Lisp** — CLTL2-compatible,
- **Standard ML** — strongly typed, polymorphic, functional.

It ran a generation of AI and cognitive-science teaching, then largely fell off the modern platform map. **We brought it back — natively — to the silicon people actually have in 2026**, and then pushed it further than the original ever went. The work builds on [W. Hebisch's Poplog sources](https://github.com/hebisch/poplog), with a great deal of history reconstructed by hand from the Internet Archive and scattered corners of the web — and it was carried out with **Claude** as a pair-porting partner, right down into the assembler.

## Three new native ports

Poplog compiles to real machine code on every backend, so a port isn't a recompile — it's a code generator, a frame contract, and an instruction-cache story per architecture. We landed three:

- **Apple Silicon / macOS (arm64)** — a native Mach-O port. Self-hosting, all four languages, terminal VED, C↔Pop callbacks, ad-hoc signed with **no entitlements required**.
- **Raspberry Pi 5 / AArch64 Linux** — validated on the Pi 5 (all four languages + saved images), written to the generic `armv8-a` baseline so it ports readily to other ARM64 boards.
- **RISC-V / riscv64 Linux** — a native RV64GC port, **self-hosting on a StarFive VisionFive** (dual SiFive U74). All four languages, saved images, terminal VED, and the FFI float ABI; the validation suite runs 14/14.

## A fifth language: Forth

Classic Poplog ships four languages. **We added a fifth — Forth — as a first-class subsystem.** It leans on Poplog's open-stack calling convention so the implementation stays tiny and genuinely native: Forth's data stack *is* the Poplog user stack, and colon definitions (`: name … ;`) **compile through Poplog's incremental compiler to machine code** — a Forth word is a real native procedure, not threaded interpreted code. `.fth` is a recognized file type and `uses forth;` drops you into a REPL alongside Pop-11, Lisp, Prolog, and ML. Its built-in testbench is 21/21 on macOS arm64 and RISC-V, and because it's pure Pop-11 it runs on **every platform Poplog does**.

## A real ELIZA

We added a faithful implementation of Joseph Weizenbaum's original **ELIZA / DOCTOR** (MIT, 1966) — not the thin teaching pattern-matcher usually shown, but the genuine engine: keyword **ranking**, **decomposition** rules with wildcards and synonym classes, round-robin **reassembly** templates, first/second-person **reflection**, keyword redirection, and **memory**. It's written in Pop-11 (an unusually good host for it) and **validated against Weizenbaum's original 1966 script**. Chat with it locally via `tools/eliza.sh`.

## Native graphics (experimental)

Poplog's graphics were historically welded to the X window system. We added an **optional native backend built on [Dear ImGui](https://github.com/ocornut/imgui)**: **Metal + Cocoa** on macOS (no X server, no XQuartz) and **SDL3 + OpenGL3** on macOS or Linux — SDL3 picks Wayland, X11, or KMS/DRM at run time, so there's no hard X11 dependency, and it even renders **headless** via Mesa software for CI. The classic `rc_graphic` turtle library is ported on top, so existing Pop-11 graphics code runs unchanged. Demos include the classic [10 PRINT](https://10print.org/) maze and a vsync-paced spinning 3D cube.

## Porting knowledge, written down

A port is only worth as much as the next person can reuse. We shipped an unusually deep set of notes — a [porting recipe](https://github.com/IoTone/poplog/blob/master/PORTING-POPLOG.md), a [guide to hosting a new language on the VM](https://github.com/IoTone/poplog/blob/master/HOSTING-LANGUAGES.md), the AArch64 frame contract, RISC-V porting notes, and forensic write-ups of specific codegen bugs (false-label leaks, tail-subtract high-word, stale I-cache SIGILLs) — so the next architecture is a documented walk, not an archaeology dig.

## Benchmarks

We published a rigorous [benchmark suite](https://github.com/IoTone/poplog/blob/master/BENCHMARKS.md): engine micro-benchmarks (calls, arithmetic, allocation/GC, incremental compilation, closures, strings) as the **median of 30 runs** with bootstrap 95% confidence intervals, across five machines — Intel i7, Apple M2, **Apple M5 Pro**, Raspberry Pi 5, and the **RISC-V** VisionFive — with Python and Perl baselines. A representative result: Poplog **runtime-compiles a procedure to machine code in ~5.5 ms on an M5 Pro** — parity with, or faster than, interpreters merely building bytecode.

## Status

Active. A self-contained **Nix flake** builds and bootstraps the whole system — all five front-ends and their saved images — from source (`nix build .#poplog`, or `.#poplog-gfx` for the graphics variant). Source, ports, docs, and benchmarks on [github.com/IoTone](https://github.com/IoTone/poplog).
