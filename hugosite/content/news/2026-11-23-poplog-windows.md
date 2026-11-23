---
title: "Poplog builds and runs on Windows 11"
date: 2026-11-23
draft: false
tags: ["poplog", "pop-11", "windows", "cygwin", "porting", "x86-64", "langpop", "language-learning"]
summary: "Our Poplog port has a fourth platform: x86-64 Windows 11, built under Cygwin from the same configure and Makefile as everywhere else. It builds itself, runs all the Poplog languages, and has a native Direct3D graphics backend. It is experimental and lives on the dev branch. Also this month: langpop asks new students what they are learning for, and has phrases for travellers."
source_url: "https://github.com/IoTone/poplog/blob/dev/INSTALL-WINDOWS.md"
hero_image: "/images/news/poplog.png"
repo_url: "https://github.com/IoTone/poplog"
related_projects:
  - "poplog"
---

[Poplog](/projects/poplog/), the classic AI development environment we brought to Apple silicon, Raspberry Pi 5 and RISC-V, now also **builds and runs on Windows 11**. The work [merged into the `dev` branch](https://github.com/IoTone/poplog/pull/80) on November 22.

## What works

Poplog on Windows is a 64-bit Cygwin program. It does not need WSL, Docker, MSYS2 or Visual Studio.

- **It builds itself.** Starting from a small bootstrap binary that ships in the repository, `./configure --with_no_x && make all` produces the full system, including the Pop-11, Lisp, Prolog and ML images.
- **The runtime is complete enough for real programs.** External C calls, DLLs, callbacks and sockets all work.
- **Native graphics.** A third Dear ImGui backend, on Win32 and Direct3D 11 with a software fallback, joins the macOS and Linux ones. It is behind an experimental configure flag.
- **The source now checks out on Windows.** Poplog has help files with names like `hash_<`, which Windows cannot store. They are renamed, and the help system maps the old names, so `HELP HASH_<` still works on every platform.

The port's own validation script passes 48 of 48 gates, and all 19 library test suites pass on the Windows machine it was built on.

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
