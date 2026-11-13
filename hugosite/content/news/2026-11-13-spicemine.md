---
title: "Spicemine — a self-hosted home for everything people version, not just code"
date: 2026-11-13
draft: false
tags: ["spicemine", "iotone-japan", "self-hosted", "version-control", "creators", "fossil", "git", "common-lisp", "ai-policy", "apache-2"]
summary: "Spicemine is our big collaboration with IoTone Japan: a self-hosted repository host for coders and creators. It wraps Fossil, git, Mercurial and Jujutsu rather than inventing its own version control, adds drag-and-drop commits, contact sheets, editions and a public journal for people who version drafts and masters instead of source files, and lets every project state its own AI policy. A companion app, Mobile Creator Life, is in progress as a members-only project."
source_url: "https://spicemine.iotj.cc/"
---

Our largest collaboration this year is with **IoTone Japan** on [**Spicemine**](https://spicemine.iotj.cc/ui/thecommons/spicemine), a self-hosted home for version-controlled work. The public instance at [spicemine.iotj.cc](https://spicemine.iotj.cc/) is running **v0.147.0**, and the project's own repository there has taken about 300 commits since it was created on October 23.

It would be easy to file Spicemine under "source control hosting" and move on. That undersells it. Code is one of the things people version. Writers version drafts, illustrators version layers, musicians version takes and masters. Spicemine is built for all of them, and for the people who would never describe what they do as "pushing a commit".

## A shell around real version control

Spicemine does not implement a version control system of its own. It hosts repositories in the engines people already trust:

- **Fossil**, **git**, **Mercurial** and **Jujutsu**, served over HTTPS and SSH
- **Lore**, a fifth engine, marked experimental on the landing page

A repository in one engine can be **mirrored** in another engine's format, so a project kept in Fossil can still be cloned by someone who only knows git. **Subs** are the reverse: read-only copies of repositories that live somewhere else. An existing project can be fetched in from its address.

The whole thing is one JVM and one directory, which also makes it one thing to back up. A backup is restored into a throwaway instance before it counts as a backup, then encrypted and sent to whichever remote you choose.

## For creators, not only coders

This is where Spicemine leaves the usual forge behind:

- **Drag-and-drop upload.** Drop files on the page and they become one commit. No client to install and no command line.
- **In-browser editing** for text.
- **Contact sheets** for directories of pictures, and viewers for files a browser cannot open by itself.
- **Editions.** A named revision, downloadable as a zip: the version you would hand to a publisher or a client.
- **A showcase** for each repository, with its README and a hero image.
- **A public journal** of short posts, 280 characters each.

Around those sit the things a team expects: personal and group spaces, roles for members, writers and admins, repositories that are private, members-only or public, scoped tokens and SSH keys, and search across spaces, projects and issues. Issues are stored as Markdown in a companion repository beside the project, so the tracker is versioned like everything else and the database only indexes it.

The interface comes in English and Japanese, with ten skins.

## Every project states its AI policy

Hosting creative work in 2026 means answering a question older forges never had to ask: may a machine take this?

Spicemine separates two things. **Exposure** says how visible a project is. **AI policy** says what an automated reader may do with it: use it, use it with attribution, ask first, or not at all. The policy is published where a crawler will actually look, in `robots.txt`, at `/.well-known/ai-policy`, in an `X-AI-Policy` response header and on the page itself.

A project that has said nothing is treated as **ask first**. The project describes this as a refusal of anonymous bulk taking, not a position against machines.

One piece is not finished, and the README says so plainly: the **Guardian**, the gate that would enforce these policies against crawlers, is designed but not built, and nothing is rate-limited yet.

## Mobile Creator Life

Spicemine has a companion: **Mobile Creator Life**, an app for creators who work from a phone more than from a desk. It is being developed as a **members-only project**, so the source is not public yet, but the Spicemine landing page already lists where it stands. Posting from anywhere, sound with captions, scheduling, a personal `/@yourname` page, and thanks and follows are marked ready. Pairing a phone with a code, alerts and live streams are marked as coming.

We will write about it properly when it opens up.

## Under the hood

Spicemine is written in **Common Lisp** on the JVM, using ABCL and a framework called **mélangej**, with Jooby and Netty underneath and JGit for the git engine. Storage is embedded SQLite by default, with PostgreSQL as an option. Every dependency is a jar from Maven Central and there are no Lisp dependencies to chase. Readers of our earlier post on [blow-cl](/news/2026-10-16-blow-cl/) will recognise the family.

## Running it

Spicemine is meant to be run by the people who use it. You need JDK 17 or newer, plus whichever engines you plan to host:

```sh
core/gradlew -p core installDist
JAVA_HOME=/path/to/jdk17+ core/build/install/spicemine/bin/spicemine-server
```

The first boot prints the instance admin token once. The supported deployment is a NixOS module, and any JVM host behind a TLS terminator will also do. Spicemine is licensed under the **Apache License 2.0**. The project says there will be no commercial release; what may be paid for is services around it.

The public instance does not offer self-serve signup yet. Invitations are issued by hand, so [get in touch](/contact/) if you would like one. In the meantime, anyone can browse [The Commons](https://spicemine.iotj.cc/ui/thecommons/spicemine) and read the [about page](https://spicemine.iotj.cc/about).
