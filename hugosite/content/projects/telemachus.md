---
title: "Telemachus"
date: 2026-08-11
draft: false
status: "active"
language: "Racket"
license: "MIT"
github_url: "https://github.com/IoTone/Telemachus"
weight: 13
featured: true
hero_visual: "alt-1"
pill: "Private AI lab"
related_news: "/news/2026-08-11-telemachus/"
summary: "A team-oriented, self-hosted, privacy-first platform for hosting AI tools and applications. Chat, research, and document translation out of the box; an SDK contract underneath; nothing leaves the building."
tags: ["ai", "self-hosted", "privacy", "racket", "llama-cpp", "rbac", "mcp", "sdk", "i18n"]
---

## What it is

**Telemachus** — the son of Odysseus — is a team-oriented, self-hosted, privacy-first platform for hosting AI tools and applications. Local-first, driven primarily by `llama-cpp` / `llama-server`, with minimal Python exposure, and open from day one. Built for teams of 1 to 1000 who want the capability without shipping their documents to somebody else's datacenter.

## The stock applications

**Chat** — token-streamed replies from a local model, admitted through a per-team concurrency governor and metered against AI quotas.

**Agentic tool use** — the agent plans, calls a tool, reads the result, and answers. One registry serves built-in tools, plugins, external MCP servers, and sandboxed out-of-process tools with declared scopes.

**Translation** — live EN↔JA with a team glossary for terminology consistency and a metered history. The same engine translates whole locale catalogs, which is how the product's own Japanese UI stays current.

## The platform underneath

Beyond the stock apps, Telemachus is an **SDK and platform**: deployers extend it with plugins — new tools and integrations, datasets, and localizations — through a stable, documented contract.

The first prototype is written in Racket, but frontend and backend are deliberately **swappable**. The durable surface is the SDK contract, the backend APIs, the security model, and the protocols — not any one implementation. A second reference implementation on the same contracts is expected later.

- **RBAC-5** — owner / admin / member / viewer within a team, plus an instance *operator* tier above them. Every API call is authorized through one service; tokens are capped by issuer-permissions ∩ scopes.
- **Document repository** — binary documents as repository objects behind an S3-compatible front door: presigned links, `CopyObject`, object versions, and indexed, searchable content.
- **PostgreSQL parity** — the unit suite runs on both SQLite and PostgreSQL, which caught two real bugs a SQLite-only suite could not see.
- **Federated compute** — a pluggable seam for handing work to remote or HPC executors alongside the local node.
- **Localized top to bottom** — one toggle re-renders the whole UI in Japanese via ICU MessageFormat catalogs, with a fallback chain and source-hash staleness detection.
- **A beta onboarding funnel** — a pre-sales lead pipeline a deployer skins and owns, with an owner-only review inbox behind one anti-abuse gate.

## Documentation that can't drift

Every screenshot in the README is produced by Playwright tours that drive a real server against a throwaway database, and CI runs the same tours on every push. Nothing in the documentation is a mockup, and nothing quietly stops working.

## Status

Active and moving fast. Source, design docs, and the full feature tour on [github.com/IoTone/Telemachus](https://github.com/IoTone/Telemachus).
