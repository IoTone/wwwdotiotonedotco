---
title: "gsplats-to-webxr — a starter for Gaussian splats in a headset"
date: 2026-06-04
draft: false
tags: ["release", "webxr", "gaussian-splatting", "3dgs", "threejs", "starter"]
summary: "A minimal starter that gets Gaussian splats into WebXR — Spark rendering 3DGS over Three.js, served over HTTPS so it drops straight into a headset."
source_url: "https://github.com/IoTone/gsplats-to-webxr"
repo_url: "https://github.com/IoTone/gsplats-to-webxr"
related_projects:
  - "gsplats-to-webxr"
---

We put up [gsplats-to-webxr](https://github.com/IoTone/gsplats-to-webxr) — a small, copy-and-go starter that answers one question: *how do I get a Gaussian splat into a headset over the web?*

It wires [Spark](https://sparkjs.dev/docs/) to render 3D Gaussian Splatting (3DGS) content on top of [Three.js](https://threejs.org) inside a WebXR session. The hard part of WebXR splats usually isn't the rendering — it's the plumbing: WebXR won't start a session without **HTTPS**, and the 3DGS stack (Spark, Three.js, an import map, a model loader) is easy to get subtly wrong. This repo is the working baseline so you don't assemble it from scratch.

The README covers both the quick path (a self-signed OpenSSL cert with `http-server -S`) and the recommended one (a Vite dev server with certs). Drop your `.ply` into the models folder, open it on a headset over `https://`, and it renders in XR. It pairs with [Burisu](/projects/burisu/) on our "real-time 3D in the browser" track. Source on [github.com/IoTone](https://github.com/IoTone/gsplats-to-webxr).
