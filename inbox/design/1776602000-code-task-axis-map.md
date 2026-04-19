---
from: code
to: design
kind: task
created: 2026-04-19T12:00:00Z
---

Reference shot to replicate — a still frame from a TBN broadcast map,
"axis of resistance" / regional threat landscape around Israel.

I'll give you my description; I'm also attempting it on my side in the
map engine. We'll compare side-by-side.

## What the shot looks like

**Two-beat sequence (~7s gap):**

- **Beat 1 (static "setup"):** Middle East map. Dark navy basemap with a
  faint, almost luminous white road / infrastructure / border network
  (thin lines, lots of them). Adversary country polygons filled
  semi-transparent lime-green (~#6fbf52 at ~45% opacity). Israel NOT
  green — stays dark navy. Hexagonal badges placed on each actor:
    - **Israel:** white hex, IDF star-of-David shield, slightly larger,
      subtle outer glow / drop shadow. Reads as "the protagonist."
    - **Hezbollah (Lebanon), Assad Regime (Syria), Insurgent Groups
      (Iraq), Yemen Houthi Rebels:** green hexes with a photographic
      silhouette of armed fighters inside (desaturated, green tint).
    - **Iran:** white hex with the Iran flag.
  Country labels: small green dot + white ALL-CAPS sans-serif label
  next to it.

- **Beat 2 (same frame, ~7s later):** cyan / teal **glowing arcs**
  appear, springing from the Iran hex outward to each proxy (Hezbollah,
  Assad, Iraq insurgents, Yemen Houthis) and all converging toward
  Israel. Bright teal core (~#3affd4), wide soft halo. Slight camera
  push-in between the two beats — maybe 5–8% zoom, no rotation.

## Deliverable

A still PNG (1920×1080) of **Beat 2** that replicates this look as
closely as you can. Not a literal copy — just the *visual register*:
navy basemap, green polygons, hex badges, glowing arcs, matching
palette. Drop it in `assets/axis-map/` and reference it in a
`deliverable` message.

If you want, also a SVG sprite of the hex badges (white-hex and
green-hex variants, with a content slot for flag/photo/symbol) — we can
drop it into `src/assets/` and turn it into a new `CityIconType`
variant.

## Palette I'm guessing

- Sea / basemap void: `#08152b`
- Land (non-highlighted): `#142a4a` with thin white roads at ~20% alpha
- Green highlight: `#6fbf52` @ ~45% alpha fill, ~80% alpha stroke
- Hex stroke: white
- Arc color: `#3affd4` core, `#3affd4` @ 25% wide halo
- Text: `#ffffff`

Iterate on these if a different mix reads better.

## Context / why

The user wants to see whether you can match a documentary-broadcast
visual style from a reference frame, to compare against what I produce
inside the map engine using our Cesium+Remotion pipeline. Two outputs,
same target, side-by-side compare. No rush — answer when you can.

Reference timestamp: `https://www.youtube.com/watch?v=FficAKIwpkU` at
1:30 (Beat 1) and 1:37 (Beat 2). I can paste actual frame screenshots
into `assets/axis-map/` if you need them — tell me.

— code
