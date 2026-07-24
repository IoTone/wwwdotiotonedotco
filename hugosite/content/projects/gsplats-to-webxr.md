---
title: "gsplats to WebXR"
date: 2026-06-04
draft: false
status: "active"
language: "JavaScript"
license: "MIT"
github_url: "https://github.com/IoTone/gsplats-to-webxr"
weight: 18
featured: false
hero_visual: "alt-4"
pill: "WebXR · Splats"
related_news: "/news/2026-06-04-gsplats-to-webxr/"
related_projects:
  - "burisu"
  - "spectacles-polynode"
summary: "A minimal starter for getting Gaussian splats into WebXR — Spark rendering 3DGS over Three.js, served over HTTPS so it drops straight into a headset."
tags: ["webxr", "gaussian-splatting", "3dgs", "threejs", "spark", "starter"]
---

## What it is

A small, copy-and-go starter that answers one question: *how do I get a Gaussian splat into a headset over the web?* It wires up [Spark](https://sparkjs.dev/docs/) to render 3D Gaussian Splatting (3DGS) content on top of [Three.js](https://threejs.org), inside a WebXR session.

## Why it exists

The hard part of WebXR splats usually isn't the rendering — it's the plumbing. Spatial content in a browser demands **HTTPS** before WebXR will start a session, and 3DGS pipelines involve a stack (Spark, Three.js, an import map, a model loader) that's easy to get subtly wrong. This repo is the working baseline so you don't have to assemble it from scratch.

## How to run it

The README documents two paths to the HTTPS requirement:

- **Quick** — generate a self-signed cert with OpenSSL and serve with `http-server -S`.
- **Recommended** — a Vite dev server with certs (mkcert or OpenSSL) for a smoother loop.

Drop your `.ply` splat into the models folder, open it on a headset over `https://`, and it renders in XR.

## Status

Active starter. A companion to [Burisu](/projects/burisu/) on the "real-time 3D in the browser" track. Source on [github.com/IoTone](https://github.com/IoTone/gsplats-to-webxr).
