---
title: "Telemachus — a private AI lab your team actually hosts"
date: 2026-08-11
draft: false
tags: ["release", "telemachus", "ai", "self-hosted", "privacy", "racket", "llama-cpp", "sdk"]
summary: "IoTone opened Telemachus: a team-oriented, self-hosted, privacy-first platform for running AI tools — chat, research, and document translation out of the box, an SDK contract underneath, and no traffic leaving the building."
source_url: "https://github.com/IoTone/Telemachus"
hero_image: "/images/news/telemachus.png"
repo_url: "https://github.com/IoTone/Telemachus"
related_projects:
  - "telemachus"
---

We opened [**Telemachus**](https://github.com/IoTone/Telemachus) — named for the son of Odysseus — a **team-oriented, self-hosted, privacy-first platform for hosting AI tools and applications**. Local-first, driven primarily by `llama-cpp` / `llama-server`, with minimal Python exposure, and open from day one. It is built for teams of 1 to 1000 who want the capability without shipping their documents to somebody else's datacenter.

## What it does out of the box

The generic application set is **chat**, **research**, and **document translation**:

- **Streaming chat** against a local model, admitted through a per-team concurrency governor and metered against AI quotas.
- **Agentic tool use** — the agent plans, calls a tool, reads the result, and answers. The same registry serves built-in tools, plugins, external MCP servers, and sandboxed out-of-process tools with declared scopes.
- **Translation** — live EN↔JA with a team glossary for terminology consistency. The same engine translates whole locale catalogs, which is how the product's own Japanese UI stays current.
- **Teams and RBAC-5** — owner / admin / member / viewer under a team, with an instance *operator* tier above them. Every API call is authorized through one service; tokens are capped by issuer-permissions ∩ scopes.
- **Localized top to bottom** — one toggle re-renders the entire UI in Japanese via ICU MessageFormat catalogs, with a fallback chain and source-hash staleness detection.

## A platform, not just an app

Beyond the stock apps, Telemachus is an **SDK and platform**. Deployers extend it with plugins — new tools and integrations, datasets, and localizations — through a stable, documented contract. The first prototype is written in **Racket**, but frontend and backend are deliberately **swappable**: the durable surface is the SDK contract, the backend APIs, the security model, and the protocols, not any one implementation.

Since launch it has grown a **document repository** with an S3-compatible front door — presigned links, object versions, indexed and searchable content — plus PostgreSQL parity alongside SQLite, and **federated compute**, the pluggable seam for handing work to remote or HPC executors.

## Screenshots that can't drift

Every image in the README is produced by Playwright tours that drive a real server against a throwaway database. CI runs the same tours on every push, so nothing in the documentation is a mockup and nothing quietly stops working.

Source, design docs, and the full feature tour on [github.com/IoTone/Telemachus](https://github.com/IoTone/Telemachus).
