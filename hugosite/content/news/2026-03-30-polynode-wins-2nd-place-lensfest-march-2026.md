---
title: "Polynode wins 2nd Place OSS Prize at Lensfest March 2026"
date: 2026-03-30
draft: false
tags: ["award", "spectacles", "polynode", "oss"]
summary: "IoTone, Inc.'s Spectacles-polynode — a backfill of HTML5 web APIs for Snap Spectacles — won the 2nd Place OSS Prize at Lensfest March 2026, run by Lenslist and Snap Inc."
source_url: "https://www.linkedin.com/pulse/iotone-inc-wins-2nd-place-oss-prize-polynode-lensfest-spectacles-7n3rc"
---

A quick note to give a little hurrah for #OSS, and to announce that we were just awarded a 2nd place prize among a group of talented developers and submissions in the March 2026 Lensfest. Special thanks to [Lenslist](https://lenslist.co) and [Snap Inc.](https://snap.com) for running the challenge.

So what is "Polynode"? The name is a combination of *polyfill* + *node.js*, and the project provides some of the missing HTML5 libraries you wish you had in Lens Studio. So what's missing from Lens Studio (thought it was JS / TS)? Glad you asked. It isn't running in a browser. It isn't built on top of node.js (though node tooling may be involved). When you start working you find a lot of APIs you would like to have are missing: no DOM, no native SVG support, a limited model for events outside the scripting components, and no 2D canvas. [Spectacles-polynode](https://github.com/IoTone/Spectacles-polynode) is an attempt to backfill some of that functionality.

## Originally we were trying to get LaTex working

For some math projects. For those who know LaTex on the web, it solidly builds on DOM, canvas, and SVG as primary output formats. We realized quickly that we'd need to solve one or all of these gaps to get there, or write a new library from scratch. We aren't in the business of math layout or typesetting. So building ports turned out to be the better path.

## EventEmitter

The first piece was the event emitter. This is used on a handful of our lenses for Snap Spectacles, and is just a nice way to add complex, flexible event handling between classes/scripts. Hand-ported.

## SpaceCanvas

Next was canvas — SpaceCanvas. It should be a drop-in replacement for any place you would normally use HTML5 canvas. It uses the WebView and some tricks the Snap team dropped on the Reddit forums. We were able to exploit those and used [Anthropic](https://www.anthropic.com)'s #Claude code to crank out a clean port once we had a viable approach. Please file bugs. It works. There are 4 samples — a general gallery, something resembling Snakes, a bad shooter, and Conway's Game of Life. SpaceCanvas runs hot and isn't efficient because WebViews overheat the Spectacles. More tuning needed but it looks good.

## SpaceSVG (the gem)

SpaceSVG converts SVG files (encoded as strings) into meshes. They look nice and run efficiently. Not fully spec-compliant yet, but it's decent — quickly you can render good-looking 2D shapes and animations. With an approach set out first, #Claude got this off the ground. We needed it to complete the LaTex port (releasing next month). It's also used in the Moire Lens "art book" project.

## SpaceDOM

The final one is SpaceDOM, a drop-in DOM replacement, useful when porting libraries to Spectacles.

---

Thanks for reading. Thanks to support from IoTone Japan for using these projects on commercial work. (Written with fingers by human slop.)
