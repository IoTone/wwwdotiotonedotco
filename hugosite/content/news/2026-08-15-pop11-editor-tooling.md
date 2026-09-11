---
title: "Pop-11 gets a tree-sitter grammar — and a Zed extension to go with it"
date: 2026-08-15
draft: false
tags: ["release", "pop-11", "poplog", "tree-sitter", "zed", "editor-tooling", "parsing"]
summary: "A tree-sitter grammar for Pop-11 that parses 95.2% of the full 270k-line Poplog tree, plus a Zed extension built on it — highlighting, outline, folding and brackets for a language whose syntax programs are allowed to extend at compile time."
source_url: "https://github.com/IoTone/tree-sitter-pop11"
repo_url: "https://github.com/IoTone/tree-sitter-pop11"
related_projects:
  - "pop11-editor-tooling"
  - "poplog"
---

Having [revived Poplog on modern silicon](/news/2026-07-24-poplog/), we ran into the next problem: forty years of Pop-11 source, and no editor on earth that knows what it is looking at. So we wrote the grammar — [**tree-sitter-pop11**](https://github.com/IoTone/tree-sitter-pop11) — and then the extension that consumes it, [**zed-pop11**](https://github.com/IoTone/zed-pop11).

## Parsing a language that redefines its own syntax

Pop-11's syntax is **user-extensible**: a program can define new syntax words at compile time. No static grammar can ever be complete, so the design goal was never completeness — it was **graceful degradation**. This grammar parses the stable core faithfully and lets everything else fall back to a flat item "soup" rather than derailing the whole file.

The core it does handle is not small:

- Comments (`;;; …` and *nesting* `/* … */`), strings, word literals in closed, `"""` and unclosed `"ml]` forms, character constants in every historical spelling including the legacy unclosed `` `7 ``, and radix numbers like `16:FF`.
- `define`/`enddefine` in all its shapes — modifiers, `:forms`, infix operator definitions, the `= expr` value form — with the defined name captured for highlighting.
- The closed set of core block syntax words and their `end…` closers, including the archaic `until … then … enduntil` loop.
- Declarations (`vars`, `lvars`, `dlocal`, `constant`, procedure typing, syntax-word name lists), `uses` in its bare, parenthesised and hyphenated forms, `exload` blocks, and `vedset` key maps where `[` is a literal token.
- **Quoting semantics** — `[ … ]` and `{ … }` quote their contents so any keyword inside is data, while `% … %` switches back to evaluation.
- The `#_IF` family of compile-time directives and `#_< … >_#`.

## Measured against the real thing

The grammar was validated against the **full Poplog tree — 1,805 files, 270,000 lines spanning 1985 to 2026**, including the syspop system dialect and the internals of the Lisp, Prolog and ML subsystems. **95.2% of files parse without errors**, and the user-facing library corpus plus every modern library parse clean.

## In the editor

[zed-pop11](https://github.com/IoTone/zed-pop11) brings that to [Zed](https://zed.dev): highlighting, outline symbols, folding, brackets and comment support for `.p`, `.ph` and `.pop11` files. It's in the Zed extension registry — search "Pop-11" in `zed: extensions`.

One honest caveat, documented in the README: **`.p` is contested**. Pascal, Gnuplot and OpenEdge all claim it, and Zed has no content sniffing. The extension takes `.p`; if that's wrong for your project, override it per-project in `.zed/settings.json`.

Both MIT. This is phase P1 of the [Poplog editor-bindings plan](https://github.com/IoTone/poplog/blob/master/poplog-language-binding-plugins.md) — the Pop-11 LSP server (real-compiler diagnostics, HELP hover, dictionary completion) already ships in the [poplog](/projects/poplog/) repo, and wiring it to Zed is the next step.
