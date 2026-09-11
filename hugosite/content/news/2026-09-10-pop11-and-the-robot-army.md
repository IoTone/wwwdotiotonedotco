---
title: "Pop-11 and the Robot Army — a free book on Poplog as an agent's command post"
date: 2026-09-10
draft: false
tags: ["release", "poplog", "pop-11", "book", "prolog", "common-lisp", "standard-ml", "forth", "ai-agents", "documentation", "cc0"]
summary: "A 31-page introduction to Poplog and Pop-11, framed around a fleet of robots and the AI agent commanding them. Every listing was executed against the tree while the text was written, and the whole thing is dedicated to the public domain under CC0."
source_url: "https://iotone.github.io/poplog/poplog-book.pdf"
hero_image: "/images/news/poplog-book.jpg"
repo_url: "https://github.com/IoTone/poplog"
book_url: "https://iotone.github.io/poplog/poplog-book.pdf"
related_projects:
  - "poplog"
  - "pop11-editor-tooling"
---

We wrote a book: [**Pop-11 and the Robot Army**](https://iotone.github.io/poplog/poplog-book.pdf) — *Poplog as the engine behind AI agents and the machines they command.* Thirty-one pages, free, and dedicated to the public domain.

It exists because [reviving Poplog](/news/2026-07-24-poplog/) produced a working system that almost nobody alive knows how to drive. The forty-year paper trail is excellent and mostly assumes you are already in a 1985 Sussex lecture theatre. This is the missing on-ramp.

## The premise

You have a fleet. Scouts, sappers, medics, haulers — a few today, a few hundred later — each one reporting telemetry, each one waiting for orders. Above them sits an AI agent that reads the reports, decides, and issues the orders. That agent needs a tool that can hold the whole picture in one place, change its own behaviour while running, and never make the fleet wait on a build.

The book argues that three properties Poplog has had since the 1980s are exactly what an agent-driven command post wants:

- **The compiler is a procedure in the running system.** Defining a new behaviour — a new order, a new triage rule — costs about **fifteen microseconds** and produces native machine code. An agent can extend its own tooling mid-mission.
- **The whole session is a value.** The heap — the fleet registry, every compiled procedure, every rule learned so far — writes to a file in milliseconds and restores in a new process. A command post that survives a restart is a file copy.
- **Five languages share it.** Prolog holds the chain of command, Forth runs on the robot, ML types the sensor model, Lisp plans — and one `?-` at the Pop-11 prompt reaches any of them.

## Everything in it was run

This is the part we care most about. **Every listing was executed against the source tree while the text was written**, on Apple Silicon; the outputs printed in the book are the outputs that came back. The full programs live in [`examples/robotarmy/`](https://github.com/IoTone/poplog/tree/master/examples/robotarmy) and each runs from the repository root:

| File | What it shows |
|---|---|
| `fleet.p` | A `Robot` Objectclass, a word-keyed registry, `muster()` on the open stack, and `obey()` — an order interpreter built on Pop-11's list matcher |
| `telemetry.p` | One pass over a fleet log: level counts, units ranked by fault, slowest operation — using Poplog's `@`-escaped regexps and default-valued properties |
| `c2.p` | The command post as an HTTP service in pure Pop-11: `GET /fleet`, `GET /status?unit=r1`, `POST /order` |
| `chain.pl` | The chain of command as Prolog relations — `can_order/2`, `reports_to/2`, `obeys/2` |
| `patrol.fth` | Robot control words in Poplog Forth, with an early `leave` |
| `signed_orders.p` | HMAC-signed orders through OpenSSL via a C shim — genuine, tampered, and replayed |

## What's covered

Eight chapters and a cheat sheet: the two-level virtual machine and why a language hosted on it inherits every port for free; a quickstart; Pop-11 fundamentals including the list matcher and the quoting trap; running the fleet; the five front-ends and how to cross between them; **hosting a language of your own** on the VM in three tiers of effort; and the C interface — `exload`, `exacc`, and the shim discipline that makes a foreign call something a robot can trust.

There are honest numbers, too. The benchmark chapter puts Poplog against CPython on identical hardware and prints the row where **Python wins** — runtime compilation, because `compile()` produces bytecode while Poplog produces machine code.

## Public domain

Text, listings, diagrams and the hand-drawn cover art are released under the **Creative Commons CC0 1.0 Universal** public domain dedication. Copy it, translate it, teach from it. The LaTeX source is in `docs/book/` with `SOURCE_DATE_EPOCH` pinned, so a rebuild is byte-identical to the published PDF.

[Read the book](https://iotone.github.io/poplog/poplog-book.pdf) · [Poplog source](https://github.com/IoTone/poplog)
