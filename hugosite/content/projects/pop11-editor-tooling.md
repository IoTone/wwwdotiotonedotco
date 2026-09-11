---
title: "Pop-11 Editor Tooling"
date: 2026-08-15
draft: false
status: "active"
language: "C · Tree-sitter Query"
license: "MIT"
github_url: "https://github.com/IoTone/tree-sitter-pop11"
weight: 9
featured: false
hero_visual: "alt-4"
pill: "Editor tooling"
related_news: "/news/2026-08-15-pop11-editor-tooling/"
related_projects:
  - "poplog"
summary: "A tree-sitter grammar for Pop-11 that parses 95.2% of the full 270k-line Poplog tree, plus a Zed extension built on it — highlighting, outline, folding, and brackets for a language whose syntax programs may extend at compile time."
tags: ["pop-11", "poplog", "tree-sitter", "zed", "editor-tooling", "parsing"]
---

## What it is

Two repositories that give Pop-11 sources a modern editing experience:

- **[tree-sitter-pop11](https://github.com/IoTone/tree-sitter-pop11)** — the grammar, with highlight, fold and textobject queries.
- **[zed-pop11](https://github.com/IoTone/zed-pop11)** — the [Zed](https://zed.dev) extension built on it: highlighting, outline symbols, folding, brackets and comments for `.p`, `.ph` and `.pop11` files. Available from the Zed extension registry.

## The hard part

Pop-11's syntax is **user-extensible** — a program can define new syntax words at compile time — so no static grammar can ever be complete. The design goal was therefore graceful degradation, not completeness: parse the stable core faithfully and let everything else fall back to a flat item "soup" rather than derailing the file.

The core it handles covers comments (including *nesting* `/* … */`), strings and word literals in their closed, `"""` and unclosed `"ml]` forms, character constants in every historical spelling, radix numbers, the full range of `define`/`enddefine` shapes, the closed set of block syntax words and their `end…` closers, declarations and `uses` forms, `exload` blocks, `vedset` key maps, the `#_IF` compile-time directives, and Pop-11's quoting semantics — where `[ … ]` and `{ … }` make their contents data and `% … %` switches back to evaluation.

## Measured, not asserted

The grammar is validated against the complete Poplog tree — **1,805 files, 270,000 lines spanning 1985 to 2026**, including the syspop system dialect and the internals of the Lisp, Prolog and ML subsystems. **95.2% of files parse without errors**; the user-facing library corpus and every modern library parse clean.

## Status

Active. v0.1 — phase P1 of the [Poplog editor-bindings plan](https://github.com/IoTone/poplog/blob/master/poplog-language-binding-plugins.md). The Pop-11 LSP server (real-compiler diagnostics, HELP hover, dictionary completion) already ships in the [Poplog](/projects/poplog/) repo; wiring it into Zed needs extension WASM and is the planned follow-up.

One documented caveat: **`.p` is contested** — Pascal, Gnuplot and OpenEdge claim it too, and Zed has no content sniffing. The extension takes `.p`; projects where that is wrong override it in `.zed/settings.json`.
