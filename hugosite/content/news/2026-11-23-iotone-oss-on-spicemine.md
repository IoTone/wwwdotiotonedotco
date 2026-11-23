---
title: "Spicemine in ten days: zine catalogs for reading apps, private spaces, a documented API — and IoTone's own space"
date: 2026-11-23
draft: false
tags: ["spicemine", "iotone-japan", "self-hosted", "zines", "opds", "search", "invitations", "api", "mercurial", "mcelixr", "pop-11"]
summary: "Spicemine has shipped more than forty releases since we introduced it, moving from v0.147.0 to v0.173.0. Zines now reach e-reader apps through catalogs that name their authors, search reads READMEs and commit messages, a space can be public, members-only or private, people join by invitation, and the API has a help page and fair-use limits. IoTone has also opened its own space there, with two new projects: McElixr and modularry."
source_url: "https://spicemine.iotj.cc/ui/iotone-oss"
hero_image: "/images/news/iotone-oss-spicemine.png"
---

[Spicemine](/news/2026-11-13-spicemine/) is the self-hosted repository host for coders and creators that we are building with IoTone Japan. When we introduced it on November 13 the public instance ran v0.147.0. Ten days later it runs **v0.173.0**, after more than forty releases.

Here is what was added, and then what we have started publishing there ourselves.

## Zines reach reading apps

Spicemine treats a zine as a first-class thing a project can publish, and most of this fortnight's work for creators went here.

- **Catalogs name the people who made a zine.** Spicemine offers its zine shelves as OPDS catalogs, the format e-reader and library apps use to find and download publications. Every entry now carries the author, artist and illustrator from the project's credits, each linked to that person's page.
- **A publishing form that checks your work.** Pick a PDF and the form draws its first eight pages in reading order, guesses the layout and takes a title from the file name. If you chose no cover, your browser makes one from page one.
- **Zines appear without a switch.** A space's page shows its projects' zines as soon as there is one. The owner can choose "always" or "never" in its place.
- **Search finds zines.** Matching zines appear as covers above the project results. If you are signed in, that includes zines in projects that are not public but that you may read.
- **A comic-book copy.** Some reading apps do not open PDFs. A project can now offer a `.cbz` copy as well, made in the creator's own browser. This one is in v0.174.0, which is in the repository and not yet on the public instance.

## Search reads more

Search already covered spaces, projects, issues and journal posts. It now reads each project's **README** and its **commit messages** as well. Results respect access: you find only what you are allowed to read. The same search is in the API.

## Who can see what, and who is in

- **A space has three settings:** public, members-only or private. A private space's page does not exist for outsiders.
- **A whole site can be walled.** An administrator can make an instance members-only, with the option to keep project showcases visible to visitors. A team can run a private host and still show its work.
- **People join by invitation.** A space's settings page lists its members and their roles, and invites new ones. Adding someone from outside the space to a project sends an invitation too. Until they accept, they have no access of any kind.
- **Requests to join are a short form.** The longer interview is now a separate option the host can turn on.
- **SSH keys can be narrowed.** A key used to stand for the whole account. It can now be limited to one project or one space, and to reading only.
- **Signing in returns you to the page you came from,** and a visitor is no longer offered buttons a visitor cannot use.

## An API with a front door

- **A help page for the API.** It explains how to get a token, gives one request to try, lists the limits this server has set, and says what each refusal means. The footer links to it.
- **Fair-use limits.** A request has a time limit and a size limit. An anonymous visitor gets a smaller share than a signed-in member, and one worker is always kept free for members. A client that goes over is told when to try again.
- **Very large listings are cut cleanly.** A file listing stops at 20,000 entries and says it was cut, on the page and in the API.

## Faster and steadier

- **Mercurial project pages are about thirteen times faster.** A page that started 45 `hg` processes now starts 5, and loads in 0.38 seconds where it took 4.9.
- **Clones are streamed.** A git or Mercurial clone used to be gathered in memory before it was sent. It is now sent as it is read, which matters on a small host.
- **The host warns early.** The health check now watches memory as well as disk, and a failed backup or offsite copy is mailed to the administrators.
- **Names keep their capitals.** A project called `McElixr` is shown and linked as `McElixr`, and any spelling of the case still finds it.
- **Mail by choice.** Follows and appreciations can send mail, off unless you turn it on.

The licence is also settled: Spicemine is under the **Apache License 2.0**, copyright IoTone, Inc., stated in the README since v0.149.1.

## IoTone's own space

It would be odd to build a host and not use it, so IoTone now has a space on the public instance: [**IoTone.co OSS**](https://spicemine.iotj.cc/ui/iotone-oss). It opens with two projects. Fittingly for a host that speaks several version control systems, one is kept in git and the other in Mercurial.

### McElixr

[**McElixr**](https://spicemine.iotj.cc/ui/iotone-oss/McElixr) is a parody AI startup sitting on a real multi-user, multi-tenant web portal, written in Elixir with Phoenix LiveView and PostgreSQL, under the MIT License. It has its own post: [McElixr — a parody AI startup on top of a real multi-tenant portal](/news/2026-11-23-mcelixr/).

### modularry

[**modularry**](https://spicemine.iotj.cc/ui/iotone-oss/modularry) is a terminal assistant for planning Eurorack modular synthesizer racks, written in **Pop-11** and run on our [Poplog](/projects/poplog/) port.

Anyone who has built a modular synth knows the questions. Will this module fit? Is there enough power on the rail? Is the case deep enough? What have I spent? modularry loads a rack file, draws the rack, and checks power, fit, depth, cost and coverage.

You can type commands as plain sentences. If you have Ollama running locally it will use a local model to understand them, and it works without one.

```sh
bin/modularry examples/racks/demo.json
```

It is early and not finished. The README counts the first five build steps as in place, it runs on Apple silicon Macs only for now, and an optional helper for ModularGrid racks has not yet been tried against the live site.

## Try it

Signup on the public instance is still by invitation. Anyone can browse the [IoTone.co OSS space](https://spicemine.iotj.cc/ui/iotone-oss) and [Spicemine's own repository](https://spicemine.iotj.cc/ui/thecommons/spicemine), and cloning needs nothing but the engine each project uses:

```sh
git clone https://spicemine.iotj.cc/iotone-oss/McElixr
hg clone https://spicemine.iotj.cc/iotone-oss/modularry
```
