---
title: "IoTone has a space on Spicemine — and two new projects in it"
date: 2026-11-23
draft: false
tags: ["spicemine", "iotone-japan", "self-hosted", "elixir", "phoenix", "pop-11", "poplog", "eurorack", "synthesizers", "mercurial"]
summary: "We now publish on Spicemine as well as GitHub. The new IoTone.co OSS space opens with two projects: McElixr, a parody AI startup sitting on a real multi-tenant web portal in Elixir and Phoenix, and modularry, a terminal assistant in Pop-11 for planning Eurorack synthesizer racks. Spicemine itself has reached v0.173.0 and is licensed under Apache 2.0."
source_url: "https://spicemine.iotj.cc/ui/iotone-oss"
hero_image: "/images/news/iotone-oss-spicemine.png"
---

[Spicemine](/news/2026-11-13-spicemine/) is the self-hosted repository host we are building with IoTone Japan. It would be odd to build one and not use it, so IoTone now has a space there: [**IoTone.co OSS**](https://spicemine.iotj.cc/ui/iotone-oss).

It opens with two projects. Fittingly for a host that speaks several version control systems, one is kept in git and the other in Mercurial.

## McElixr: artisanal intelligence, mass-produced

[**McElixr**](https://spicemine.iotj.cc/ui/iotone-oss/McElixr) is a joke with a serious skeleton.

The joke is a parody AI startup. You order an "elixir" and receive a receipt full of buzzwords.

The skeleton is a real multi-user, multi-role, multi-tenant web portal and JSON API, written in **Elixir** with **Phoenix LiveView** and **PostgreSQL**. It has the parts every business application needs and nobody enjoys writing twice:

- Sign-in by email and password or by magic link
- Three account types: solo, team and partner
- Organisations, roles and an audit trail
- An API with keys, under `/api/v1`
- An idle timeout and a plan menu (which charges nothing)
- English, Spanish and Japanese

To run it, you need PostgreSQL, then `mix setup` and `mix phx.server`.

The README is clear that this is a starter, not a finished product. The legal pages are placeholders, the Spanish and Japanese translations are machine-made, there are no payments, and there is no two-factor sign-in or single sign-on yet.

## modularry: plan a synthesizer rack from the terminal

[**modularry**](https://spicemine.iotj.cc/ui/iotone-oss/modularry) is a terminal assistant for planning Eurorack modular synthesizer racks, written in **Pop-11** and run on our [Poplog](/projects/poplog/) port.

Anyone who has built a modular synth knows the questions. Will this module fit? Is there enough power on the rail? Is the case deep enough? What have I spent? modularry loads a rack file, draws the rack, and checks power, fit, depth, cost and coverage.

You can type commands as plain sentences. If you have Ollama running locally it will use a local model to understand them, and it works without one.

```sh
bin/modularry examples/racks/demo.json
```

It is early. The README counts the first five build steps as in place, it runs on Apple silicon Macs only for now, and an optional helper for ModularGrid racks has not yet been tried against the live site.

## Spicemine itself

The host has kept moving since we introduced it ten days ago:

- The public instance is on **v0.173.0**, up from 0.147.0.
- The licence is now stated in the README: **Apache License 2.0**, copyright IoTone, Inc.
- The project's own repository is past 340 commits.

Signup on the public instance is still by invitation. Anyone can browse the [IoTone.co OSS space](https://spicemine.iotj.cc/ui/iotone-oss), and cloning needs nothing but the engine each project uses:

```sh
git clone https://spicemine.iotj.cc/iotone-oss/McElixr
hg clone https://spicemine.iotj.cc/iotone-oss/modularry
```
