---
title: "The pop11 Claude skill — a scripting engine that never starts cold"
date: 2026-10-27
draft: false
tags: ["pop-11", "poplog", "claude-skill", "ai-agents", "scripting", "performance", "saved-images"]
summary: "The pop11 skill gives Claude a live Pop-11 session that persists across tool calls: helpers compile to native code in microseconds, repeat tasks cost 1–2 ms instead of a 23 ms process spawn, and the whole session — state plus compiled code — saves to a ~200 KB image that restores in 8 ms. Here's how to use it, what it unlocks, and the measured numbers."
source_url: "https://github.com/IoTone/poplog/tree/master/.claude/skills/pop11"
hero_image: "/images/news/pop11-claude-skill.png"
repo_url: "https://github.com/IoTone/poplog"
related_projects:
  - "poplog"
  - "pop11-editor-tooling"
---

Every Poplog release since August has shipped with something we have never properly written up: the [**pop11 Claude skill**](https://github.com/IoTone/poplog/tree/master/.claude/skills/pop11). It changes how an AI agent scripts on your machine. Instead of spawning a fresh interpreter for every task — pay startup, pay imports, redefine everything, throw it all away — the skill keeps **one live Pop-11 session running across tool calls**. Helpers are defined once, compiled to native machine code on the spot, and every task after that is a one-line call into an already-warm engine.

One line installs it, runtime included, on macOS arm64 or Linux x86_64 / aarch64 / riscv64:

```sh
curl -fsSL https://raw.githubusercontent.com/IoTone/poplog/master/tools/install-skill.sh | sh
```

## How it's used

The skill is built around `popsession`, a small CLI that manages named, persistent engine sessions:

```sh
popsession start --name mytask            # boot the live session (~50 ms)
popsession send  --name mytask -f helpers.p   # define this session's tools
popsession send  --name mytask -c 'scan_logs("/var/log/app");'
popsession checkpoint --name mytask data/scan-v1.psv   # ~20 ms, ~200 KB
popsession restore    --name mytask data/scan-v1.psv   # everything back, compiled
```

In practice you rarely type this yourself — Claude reads the skill's instructions and drives the session: it writes a `.p` file of `define`s for the session's recurring work, sends it once, then fires one-line calls at it for the rest of the conversation. A Pop-11 error (a *mishap*) prints its diagnostics with file and line and **the session survives** — fix the chunk and resend. Redefining a procedure mid-session takes about 60 microseconds and produces fresh native code, so iterating on a helper is free.

Every `send` ends with a 🌈 timing line — this run, the session total, the all-time total — so the cost of the scripting layer is always visible.

## What it unlocks

- **Repeat tasks at memory speed.** Scan these logs every time X happens, recompute this report, transform each batch — after the first send, each repetition is a procedure call into compiled code, not a process launch.
- **Native SQLite and HTTPS.** `build-popsqlite` and `build-popcurl` compile small C shims once; after that, `sqlite_query` runs **about 180× faster than spawning the `sqlite3` CLI per query** (measured: a 52-query report pass in 6.5 ms against 435 ms of CLI spawns), and `http_get`/`http_post` work without an external process.
- **A built-in regexp engine** compiled per pattern — define the compiled matcher once, reuse it at native speed for the whole session.
- **A cross-project toolkit.** Sessions can load ready-made `.p` tools from `~/pop11-tools/` — log triage, API grep, report generators built in past sessions — in about 20 ms each. Tools that prove reusable get promoted there, so the toolkit compounds across projects.

## Why Pop-11, of all languages

The skill is possible because of two properties Poplog has had since the 1980s, the same ones [*Pop-11 and the Robot Army*](/news/2026-09-10-pop11-and-the-robot-army/) is built around:

1. **The compiler is a procedure in the running system.** `define` doesn't queue a build — it emits native machine code in roughly ten microseconds and the new procedure exists immediately. An agent can grow its own tooling mid-task at zero perceptible cost.
2. **The whole session is a value.** The heap — every variable, every data structure, every compiled procedure — writes to a saved image and restores into a new process with everything intact. No other mainstream scripting engine can hibernate a warm process to disk and wake it up later.

Add the mishap system (errors report and return to the prompt rather than killing the process) and you have an engine built for exactly this: a long-lived, incrementally-grown, crash-tolerant workbench.

## The numbers, across a session and across restarts

The claim isn't raw speed — it's that **retention beats process-per-task**, and that Pop-11 retains better than anything else. The [bench-skill harness](https://github.com/IoTone/poplog/tree/master/tools/bench-skill) measures four modes over repeated small tasks (log scanning + a tight loop, and a recursion-heavy compute task). Medians on an Apple M5-class machine, CPython 3.14:

| Mode | glue task | compute task | setup (once) | live redefine |
|---|---|---|---|---|
| Python, process per task | 23.0 ms | 19.6 ms | paid every task | paid every task |
| Python, persistent process | 7.5 ms | 3.2 ms | 24–27 ms | 0.08 ms |
| **Pop-11, persistent session** | **1.4 ms** | **1.6 ms** | 27–32 ms | **0.06 ms** |

Over a modelled one-hour session firing a task every 30 seconds, that is **2.4–2.8 seconds** of scripting overhead for cold Python against **0.2 seconds** for the warm Pop-11 session. Retention helps Python too (about 3×) — Pop-11's edge is that its warm tasks are 2–5× cheaper still, because the tight loops run as compiled native code.

The part no warm Python process can match is what happens at the end of the day. A session with compiled procedures and mutated heap state saves to a **~200 KB** `.psv` image and restores — state intact, procedures still native — in a **7.8 ms** total process lifecycle. A warm Python exec-server dies with its process; a Pop-11 session is a file. On a host system that Claude returns to across days of sessions, that means the second session starts where the first one finished: the helpers, the parsed datasets, the built indexes — all of it back, already compiled, for the cost of reading 200 KB.

[The skill](https://github.com/IoTone/poplog/tree/master/.claude/skills/pop11) · [bench-skill harness](https://github.com/IoTone/poplog/tree/master/tools/bench-skill) · [latest release](https://github.com/IoTone/poplog/releases)
