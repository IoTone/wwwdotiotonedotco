---
title: "Poplog comes to Windows 11 — the first 64-bit Windows build, and our fifth platform"
date: 2026-11-23
draft: false
tags: ["poplog", "pop-11", "windows", "cygwin", "porting", "x86-64", "benchmarks", "langpop", "language-learning"]
summary: "Until now, running a current Poplog on a Windows PC meant running Linux: WSL or a virtual machine. Our port changes that. Poplog now builds itself and runs on x86-64 Windows 11 as a Windows program, the first 64-bit Windows Poplog there has been, with native Direct3D graphics. On the same machine its compiled code runs five to nine times faster than Python on calls, loops and list building. That makes five platforms: three Linux architectures, macOS on Apple silicon, and Windows."
source_url: "https://github.com/IoTone/poplog/blob/dev/INSTALL-WINDOWS.md"
hero_image: "/images/news/poplog-windows.png"
repo_url: "https://github.com/IoTone/poplog"
related_projects:
  - "poplog"
---

[Poplog](/projects/poplog/), the classic AI development environment, now **builds and runs on Windows 11**. The work [merged into the `dev` branch](https://github.com/IoTone/poplog/pull/80) on November 22.

## Why this one matters

For years, the honest answer to "how do I run Poplog on my Windows PC?" has been "run Linux". You installed Ubuntu under WSL or in a virtual machine and ran the Linux build inside it. Poplog on Windows was really Poplog on Ubuntu.

There was a Windows version once: a 32-bit port for Windows NT, decades ago. Traces of it survive in the source, but it was never carried forward to 64 bits and nothing of it could be reused. So this is, as far as we know, **the first 64-bit Windows Poplog**. It is a Windows program that needs no Linux anywhere on the machine.

## Five platforms

Windows brings the count of platforms our port supports to five:

| Operating system | Architecture | Tested on |
|---|---|---|
| Linux | x86-64 | Intel desktop |
| Linux | AArch64 | Raspberry Pi 5 |
| Linux | RISC-V (riscv64) | StarFive VisionFive |
| macOS | Apple silicon (arm64) | M2, M5 Pro |
| **Windows 11** | **x86-64** | **Intel laptop** |

All five build from the same `configure` and `Makefile`.

## What works

Poplog on Windows is a 64-bit program built with Cygwin, a toolkit that lets Unix software run as ordinary Windows programs. It does not need WSL, Docker, MSYS2 or Visual Studio.

- **It builds itself.** Starting from a small bootstrap binary that ships in the repository, `./configure --with_no_x && make all` produces the full system, including the Pop-11, Lisp, Prolog and ML images.
- **The runtime is complete enough for real programs.** External C calls, DLLs, callbacks and sockets all work.
- **Native graphics.** A third Dear ImGui backend, on Win32 and Direct3D 11 with a software fallback, joins the macOS and Linux ones. It is behind an experimental configure flag.
- **The source now checks out on Windows.** Poplog has help files with names like `hash_<`, which Windows cannot store. They are renamed, and the help system maps the old names, so `HELP HASH_<` still works on every platform.

The port's own validation script passes 48 of 48 gates, and all 19 library test suites pass on the Windows machine it was built on.

## How fast is it?

We ran our standard engine benchmarks on a 2022 Dell laptop (Intel Core i5-12500H) under Windows 11, against Python 3.12 from python.org and Perl 5.44 on the same machine. Poplog compiles Pop-11 to machine code, and it shows:

| Workload | Poplog on Windows 11 | Python 3.12 | Perl 5.44 |
|---|---|---|---|
| Procedure calls | 10.1 ms | 5.4× slower | 13.2× slower |
| Integer loop, 10 million steps | 46.6 ms | 5.1× slower | 2.4× slower |
| Building lists | 7.2 ms | 9.2× slower | not measured |
| A million closures | 34.0 ms | 1.3× slower | not measured |
| Garbage collection | 21.1 ms | 3.6× faster | not measured |
| String handling | 0.8 ms | 1.5× faster | not measured |
| Compiling 500 procedures | 57.2 ms | 10× faster | not measured |

Poplog wins clearly on calls, arithmetic and allocation. Python wins on garbage collection, strings and compile time, though the last row is not like for like: Poplog is producing machine code there, while Python is building bytecode. This is the same pattern Poplog shows on every other platform we have measured.

Each figure is a median with run-to-run variation under 3%, measured with every program pinned to one performance core. These numbers compare languages on one Windows machine. They are not a Windows-against-Linux comparison, which would need the same machine booted both ways. The method and the full table are in [BENCHMARKS.md](https://github.com/IoTone/poplog/blob/dev/BENCHMARKS.md).

## Try it

From PowerShell:

```
git clone --branch windows-checkout https://github.com/IoTone/poplog.git
cd poplog
powershell -ExecutionPolicy Bypass -File tools\port-windows\setup-cygwin.ps1
```

The script installs Cygwin with the right packages and needs no administrator rights. The remaining steps are in [INSTALL-WINDOWS.md](https://github.com/IoTone/poplog/blob/dev/INSTALL-WINDOWS.md). The guide puts the whole process at about ten minutes, most of it the Cygwin download.

## What to know first

This is an **experimental** port, and the project is plain about how far the testing goes:

- It has been built and validated on one machine: Windows 11 Home with Cygwin 3.6.12.
- It is not in a binary release yet, and the default branch still does not check out on Windows.
- Graphics mouse input, panels and resizing have not been tried by hand.

The change is not confined to Windows code. It touches shared x86-64 assembly and the build tools, so the branch was rebuilt and re-tested on macOS, x86-64 Linux, the Raspberry Pi 5 and RISC-V before merging. All of their library suites pass.

How the port works is written up in [PORTING-X86-64-WINDOWS.md](https://github.com/IoTone/poplog/blob/dev/PORTING-X86-64-WINDOWS.md), for the next person who wants to take Poplog somewhere new.

## Meanwhile, in langpop

[langpop](/news/2026-11-13-langpop/), the Japanese and English tutor that runs on Poplog, picked up three changes that make it friendlier to people who are not studying for an exam:

- **It asks what you are learning for.** A new student chooses between a test, a trip, talking with people, or reading. The answer changes which criteria hold a level shut and how much listening you get.
- **Phrases for travellers.** Someone learning for a trip needs to find the bathroom, check in and ask for a platform. They now hear those phrases from the first sitting.
- **Placement that places.** If you have studied before, the tutor starts above where it expects you to be and lets your misses locate you, the way a good teacher does. Passing at one level counts for every level below it.

Source is on [github.com/IoTone/pop-11-langpop](https://github.com/IoTone/pop-11-langpop).
