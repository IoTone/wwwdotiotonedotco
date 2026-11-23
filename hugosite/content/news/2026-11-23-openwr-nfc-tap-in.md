---
title: "OpenWR comes back to life — NFC taps in XR, a camera remote on your face, and an e-paper backstage pass"
date: 2026-11-23
draft: false
tags: ["openwr", "open-hardware", "wearables", "snap-spectacles", "nfc", "esp32", "e-paper", "xr", "forth"]
summary: "OpenWR, our open hardware standard for wearables, has more than a hundred new commits on its dev branch. The newest is NFCTapInXR, a Spectacles lens that turns a tap on an NFC tag into something in the air. Alongside it: LightScopeXR, a Sony camera remote you wear; SubverseReader, a $50 e-paper reader shaped like a backstage pass; and Hiroglass, an open design for XR displays that clip onto the eyewear you already own."
source_url: "https://github.com/IoTone/OpenWR/tree/dev"
hero_image: "/images/news/openwr-subversereader.jpg"
repo_url: "https://github.com/IoTone/OpenWR"
related_projects:
  - "openwr"
  - "espidforth"
  - "project-magnet"
---

[**OpenWR**](https://github.com/IoTone/OpenWR) is our open hardware standard for wearable devices. Its premise is simple: things you wear should work together the way a jacket works with its liner, with no account to create, no cloud to depend on, and no company able to switch your gear off.

The main branch had been quiet since early 2025. The [`dev` branch](https://github.com/IoTone/OpenWR/tree/dev) is another story: more than a hundred commits since late October, across four new projects. Everything below lives there.

## NFCTapInXR: tap a tag, see something appear

The newest project, finished this week. [**NFCTapInXR**](https://github.com/IoTone/OpenWR/tree/dev/projects/apps/NFCTapInXR) is a lens for Snap Spectacles that plays a scene in the air when you tap an NFC tag on a small reader.

**[Watch the 30-second video](https://youtu.be/uXBH_5CcVdo)**

Four demo scenes show what a tap can mean:

| Tap | What appears |
|---|---|
| A trading card | An original creature card turns to face you. Pinch it to pick it up and move it. |
| A sign-in badge | A spinner runs through three steps, then confirms the session is secured. |
| A 3D model | Scan hoops sweep upward while a model spins into existence. |
| A transit pass | The pass slides in and its balance counts down by the fare. When it can't pay, it tops itself up. |

The reader is about as cheap as hardware gets: an M5Stack ATOM Matrix and a PN532 NFC board, joined by four jumper wires. It sends each tap to the glasses over Bluetooth, with no pairing step and no internet.

The lens only needs a tag's ID, so nothing has to be written to the tag. Blank stickers work, and so do tags that already hold a link. Tap four unknown tags and the lens learns them in order. The README lists which tag types work and which don't. Phones and bank cards don't, because they show a new random ID every time. We buy our tags from [Tagstand](https://www.tagstand.com/), which sells NXP stickers, cards and fobs.

## LightScopeXR: a camera remote you wear

[**LightScopeXR**](https://github.com/IoTone/OpenWR/tree/dev/projects/apps/LightScopeXR) puts the controls of a Sony α7R III on Spectacles: shutter, autofocus, record, f-stop, shutter speed, ISO and exposure compensation, with a low-resolution look through the viewfinder.

The glasses can't speak the camera's Wi-Fi protocol, so a pocket-sized M5StickC sits in between, talking Bluetooth to the glasses and Wi-Fi to the camera. This month the project grew two companions:

- **Scout**, a small ESP32 camera that acts as a second shooter.
- **ReelHub**, a hub that finds the cameras on the local network and fires them together. The glasses shoot when it fires, and every shot lands on one shared reel.

The firmware for all three is written with [ESPIDFORTH](/projects/espidforth/), our Forth for ESP32. The [project log](https://github.com/IoTone/OpenWR/blob/dev/projects/apps/LightScopeXR/LOG.md) is worth reading for the dead ends alone, including the discovery that the camera drops any client five seconds after it joins unless that client starts the live view.

## SubverseReader: an e-paper reader on a lanyard

[**SubverseReader**](https://github.com/IoTone/OpenWR/tree/dev/projects/prototypes/SubverseReader_REV1) is a wearable e-paper reader the size of a backstage pass, pictured above. Sync zines, ebooks and PDFs from your phone, then read on the pass with the phone off, for days or weeks per charge.

The target price is **$50 or less** per unit, about half of what the cheapest e-paper readers sell for. The first design round covers sixteen variants, with a parts list, a battery-life estimate and a render for each. The options include a front light, a four-colour panel, sizes that match stock backstage passes, and one that collects a zine when you tap it on an NFC tag. Two of them, the Dial Pass and the Setlist, now have printable enclosures.

## Hiroglass: XR for the eyewear you already own

[**Hiroglass**](https://github.com/IoTone/OpenWR/tree/dev/projects/prototypes/Hiroglass_REV1) is the long-range one: an open hardware design for XR displays that attach to existing glasses, goggles and helmets. The first version is a heads-up display, aimed at under $300 and built from parts anyone can order.

There is no hardware yet. What is published is the thinking: a research report on open approaches to XR optics, seven concept sheets, and parts lists checked for buildability in both the US and Japan. The newest concept, **Rail**, treats someone else's goggles as a platform to mount tools on.

## Also on the branch

- **Switchback**, the OpenWR phone app, which pairs with and updates the goggl1 ski-goggle display. Its look changes with the weather the goggle reports.
- **SwitchbackXR**, the same trail app on Spectacles, built in three days for a developer meetup. NFCTapInXR and LightScopeXR both started as copies of it.

## Where this is going

The open issues on the repository describe a set of demos being prepared for CES. Expect this branch to keep moving. The code is at [github.com/IoTone/OpenWR](https://github.com/IoTone/OpenWR/tree/dev); remember to switch to the `dev` branch.
