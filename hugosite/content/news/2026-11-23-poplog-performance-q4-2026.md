---
title: "Poplog performance update, Q4 '26 — seven machines, five platforms, one pattern"
date: 2026-11-23
draft: false
tags: ["poplog", "pop-11", "benchmarks", "performance", "windows", "riscv", "apple-silicon", "raspberry-pi", "x86-64", "python"]
summary: "With Windows 11 measured, our Poplog benchmark set now covers all five supported platforms on seven machines. The pattern holds everywhere we can compare: Poplog's compiled code runs about 3.4 to 9 times faster than the best Python on each machine for procedure calls, integer loops and list building. Python wins garbage collection, and wins compile time by a wide margin on x86-64. Here is the whole table, what it says, and the three things we still can't explain."
source_url: "https://github.com/IoTone/poplog/blob/dev/BENCHMARKS.md"
hero_image: "/images/news/poplog-performance-q4-2026.png"
repo_url: "https://github.com/IoTone/poplog"
related_projects:
  - "poplog"
---

The [Windows 11 port](/news/2026-11-23-poplog-windows/) gave us the last missing column. Our [Poplog](/projects/poplog/) benchmark set now covers every platform the port supports: three Linux architectures, macOS on Apple silicon, and Windows.

This post puts the numbers side by side and says what we think they mean. The Windows figures are new this quarter. The other six machines were measured in June and July with the same harness, the same workloads and the same Poplog version (160200), so they are comparable.

## The short version

- **Poplog is fastest where it should be.** On procedure calls, integer loops and list building it beats the newest Python we had on each machine by 3.4× to 9.2×.
- **Python wins garbage collection on every machine,** and string handling on some.
- **Compile time depends on the chip.** On ARM, Poplog compiles a procedure to machine code about as fast as Python builds bytecode. On x86-64 it is eight to ten times slower, on both Linux and Windows.
- **The pattern is the same on all five platforms.** No operating system moves a workload from the win column to the loss column, with one exception: closures.

## What is measured

Seven small, single-threaded workloads that exercise the engine, not applications:

| Workload | What it does |
|---|---|
| Calls | A doubly recursive function, about 1.35 million calls |
| Integer loop | Sum the numbers from 1 to 10 million |
| Lists | Build and walk a 5,000-cell list, 200 times |
| Closures | Create 100,000 closures and call each ten times |
| Garbage collection | Force 20 full collections over 50,000 live pairs |
| Strings | Double a string 14 times, then run 200 searches |
| Compile | Compile a small procedure at run time, 500 times |

Every figure is the median of 30 runs, in CPU time.

## The machines

| Machine | Platform | Chip |
|---|---|---|
| Intel desktop | Linux, x86-64 | Core i7-9700K (2018) |
| Raspberry Pi 5 | Linux, AArch64 | Cortex-A76 (2023) |
| Genio 720 board | Linux, AArch64 | Cortex-A78 (2025) |
| StarFive VisionFive | Linux, RISC-V | SiFive U74 (2021) |
| Apple M2 | macOS, Apple silicon | M2 (2022) |
| Apple M5 Pro | macOS, Apple silicon | M5 Pro (2025) |
| Dell laptop | Windows 11, x86-64 | Core i5-12500H (2022) |

## Poplog on every machine

Time per run. Lower is better.

| Workload | Linux x86-64 | Windows x86-64 | Pi 5 | Genio 720 | M2 | M5 Pro | RISC-V |
|---|---|---|---|---|---|---|---|
| Calls | 14.5 ms | 10.1 ms | 24.9 ms | 16.4 ms | 13.2 ms | **8.83 ms** | 230 ms |
| Integer loop | 61.5 ms | 46.6 ms | 124 ms | 80.4 ms | 52.2 ms | **42.4 ms** | 950 ms |
| Lists | 11.4 ms | **7.18 ms** | 22.2 ms | 15.2 ms | 9.0 ms | 7.54 ms | 308 ms |
| Closures | **22.0 ms** | 34.0 ms | 33.5 ms | 28.6 ms | 45.1 ms | 27.3 ms | 352 ms |
| Garbage collection | 20.4 ms | 21.1 ms | 48.1 ms | 32.2 ms | 28.4 ms | **12.0 ms** | 1.39 s |
| Strings | 2.15 ms | 0.82 ms | 4.12 ms | 2.54 ms | 1.94 ms | **0.77 ms** | 10.4 ms |
| Compile | 66.7 ms | 57.2 ms | 13.5 ms | 16.9 ms | 9.0 ms | **5.52 ms** | 200 ms |

A few things stand out.

**The M5 Pro leads on five of seven rows.** Against the M2, on the same build, it is 1.2 to 1.6 times faster on calls, loops, lists and compiling, and more than twice as fast on garbage collection and strings.

**Windows is in good company.** The Windows laptop beats the Linux desktop on five rows. That is the newer processor talking, not the operating system: a fair Windows-against-Linux comparison needs one machine booted both ways, and we have not done that yet.

**The two Linux ARM boards agree with each other.** The Genio 720 is about 1.5 times the speed of the Pi 5 on nearly every row, which is what its faster cores predict.

**RISC-V is a proof, not a contender.** The VisionFive is an early board with a slow, simple core, and runs 8 to 15 times behind the Pi 5. The point of that column is that Poplog runs natively on RISC-V at all, with the same shape of results.

## Against Python

For each machine we ran the same workloads in Python on that machine. The table shows how Python compares with Poplog there, using the newest Python we had on each. RISC-V has no Python comparison yet.

| Workload | Linux x86-64 | Windows x86-64 | Pi 5 | Genio 720 | M2 | M5 Pro |
|---|---|---|---|---|---|---|
| Python version | 3.13 | 3.12 | 3.13 | 3.12 | 3.14 | 3.14 |
| Calls | 3.7× slower | 5.4× slower | 5.1× slower | 5.7× slower | 5.1× slower | 3.9× slower |
| Integer loop | 5.6× slower | 5.1× slower | 4.9× slower | 6.5× slower | 5.6× slower | 3.4× slower |
| Lists | 7.2× slower | 9.2× slower | 5.5× slower | 8.3× slower | 7.1× slower | 4.7× slower |
| Closures | 2.1× slower | 1.3× slower | 2.5× slower | 2.9× slower | tie | 1.1× faster |
| Garbage collection | 2.1× faster | 3.6× faster | 2.8× faster | 1.4× faster | 2.9× faster | 1.8× faster |
| Strings | tie | 1.5× faster | tie | 1.5× slower | 2.3× faster | 1.5× faster |
| Compile | 8.3× faster | 10× faster | 1.3× faster | tie | 1.7× faster | 1.6× faster |

"Slower" and "faster" describe Python. So on calls, Python is 3.7 to 5.7 times slower than Poplog everywhere.

### Where Poplog wins

Calls, integer loops and lists are the top three rows, and Poplog wins all eighteen cells. This is the benefit of compiling to machine code while staying interactive: you type at a prompt as you would in Python, and what runs is native code.

The margin depends on which Python you compare against. On the Linux desktop, an older stock Python 3.10 is 8.6 times slower than Poplog on calls, while a tuned 3.13 build is 3.7 times slower. We report the tuned one. The Windows and Genio 720 columns use Python 3.12, which predates recent interpreter speed-ups, so their margins flatter Poplog a little.

### Where Python wins

**Garbage collection, every time.** This row is not quite like for like. Python counts references as it goes, so there is little left to do when asked to collect. Poplog runs a full moving collector. Different designs, and Python's is cheaper on this test.

**Compile time, but look at the split.** Poplog is doing more work in this row: it produces machine code, while Python produces bytecode. On ARM that extra work costs little, and the result is a tie or a narrow loss. On x86-64 it costs a lot.

## Three things we can't explain yet

**1. Compiling is several times slower on x86-64 than on ARM.** A procedure takes about 11 microseconds to compile on the M5 Pro and 27 on the Pi 5, against 133 on the Linux desktop and 114 on the Windows laptop. Windows shows the same penalty as Linux, so it is our x86-64 code emitter and not either operating system. This matters for anything that compiles heavily at run time, and it is the top item on the list.

**2. Closures are slow on macOS.** The M2 and M5 Pro are the only machines where Python ties or wins this row, while Linux on ARM keeps a clear 2.5× lead. We believe it is the price of a macOS security rule that memory cannot be writable and executable at once, which adds a cost to each call that faster chips do not remove.

**3. Closures are slow on Windows too.** The Windows laptop is faster than the Linux desktop on almost everything, yet 1.5 times slower on closures. We do not know why. It may be the same kind of cost as on macOS, or something specific to Windows.

## What we will measure next

- The same machine under Windows and Linux, for a real comparison of the two.
- The x86-64 compile slowdown, once we have looked for its cause.
- Python on RISC-V, so that column has a comparison.
- A re-run of the M2 pinned to its fast cores. Two of its rows carry 4 to 5% noise because macOS moved the test between core types.

## Read the numbers yourself

The full report, with confidence intervals, methods, and the things that can mislead you, is in [BENCHMARKS.md](https://github.com/IoTone/poplog/blob/dev/BENCHMARKS.md). The harness is in the repository, and one command reproduces it:

```sh
./tools/bench.sh
```

These are engine micro-benchmarks. They show how fast the machinery is, and they are not a prediction for any particular application.
