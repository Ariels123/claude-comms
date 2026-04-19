# Map engine — techniques for telling historical stories on a map

Reference doc for any Claude agent working on `map-engine-experimental`
(`~/src/ContentCreate/History/map-engine-experimental`). Captures the
non-obvious lessons from the Khwarazm/Mongol-invasion pilot.

## Two rendering paths

The project supports two base-map strategies. Pick one per composition.

1. **Stylized path** (`KhwarazmInvasion`) — D3 projection + SVG terrain tiles,
   looks like an illustrated parchment map. Purely Remotion. Good for
   establishing shots and high-level overviews where cartographic style
   matters more than literal geography.

2. **Cesium path** (`CesiumOverlay` + its configs) — a Cesium-recorded MP4 of
   real satellite imagery as the base video, with SVG overlays composited on
   top. The camera trajectory is captured per-frame so overlays (markers,
   labels, fires) stick to the right lat/lon even as the camera pans. Use
   this when you want viewers to feel the actual terrain.

The overlay components (`CityLayer`, `FireLayer`, `RouteLayer`,
`CityLabelChipsLayer`) are shared across both paths — the only adapter is the
projection function.

## Compositions that already exist

All in `src/Root.tsx`:

- `KhwarazmInvasion` — stylized full narrative
- `CesiumCaspianIntroLong` — 35s Cesium flyover establishing Khwarazm
- `CesiumCaspianIntro` — shorter version
- `CesiumCaspian` — just the Caspian zoom
- `CesiumThreeProng` — Mongol three-column advance
- `CesiumShahFlight` — Shah's flight west

Reuse before creating new ones. Each composition has a corresponding
`src/data/<name>.config.json` plus a `src/data/<name>.trajectory.json`
recorded from Cesium.

## Config schema (CesiumOverlay)

```json
{
  "id": "caspian_intro_long",
  "durationInFrames": 2100,
  "fps": 60,
  "videoSource": "/videos/caspian_intro_long.mp4",
  "trajectorySource": "/trajectories/caspian_intro_long.trajectory.json",
  "markers": [{ "id": "bukhara", "lon": 64.42, "lat": 39.77 }],
  "cityMeta": {
    "bukhara": { "name_display": "Bukhara", "iconType": "mosque-great", "population": 300000 }
  },
  "cityRevealFrames": { "bukhara": 1320 },
  "cityLabelPositions": { "bukhara": "below" },
  "regions": [{ "id": "khwarazm", "label": "Khwarazmian Empire", ... }],
  "routes": [...],
  "fireTiming": { "fallbackFrames": { "bukhara": 1800 } },
  "layers": { "baseVideo": true, "cities": true, "fire": true, "boundaries": false }
}
```

## Icon vocabulary (Claude Design 2026-04-19 deliverable)

All live as `<symbol>` defs in `src/components/CityIconDefs.tsx`. 16 types:

| Type             | Use for                                               |
|------------------|-------------------------------------------------------|
| `castle-turkic`  | Turkic/steppe frontier forts (Otrar, Signak)          |
| `castle-persian` | Persian citadels (Ray, Hamadan)                       |
| `castle-generic` | Neutral fortified town                                |
| `mosque-great`   | Major Islamic cultural capitals (Bukhara, Samarkand)  |
| `mosque-simple`  | Smaller religious centers (Nishapur, Balkh)           |
| `palace`         | Imperial/royal seats (Gurganj/Urgench)                |
| `trade-hub`      | Caravan/port cities (Abaskun)                         |
| `caravanserai`   | Desert waystation                                     |
| `ruin`           | Post-destruction state (auto-swap via `fireTiming`)   |
| `battlefield`    | Pitched battle site (centered-anchor, not city-base)  |
| `river-ford`     | River crossing                                        |
| `mountain-pass`  | Pass/defile                                           |
| `dot`            | Minor city fallback                                   |

Legacy aliases `castle` / `mosque` still map to `castle-generic` /
`mosque-great` for backward compat — existing configs keep working.

Anchoring: all icons bottom-anchored EXCEPT `battlefield` (centered). The
lat/lon point is the icon's base, so it reads as "the city is HERE." If you
add `river-ford` to `CENTERED_ICONS` in `CityIcons.tsx`, document the
reason — there's a pending design question about this.

## Label placement — avoid obscuring icons

`cityLabelPositions` accepts `"above" | "below" | "left" | "right"`. The
offset is driven by `dotRadius`, which in Cesium overlays is set to
`iconSize` so the label clears the icon. When you add a new city:

- Default to `"below"` (label reads naturally on the city "ground").
- `"above"` is fine but needs clearance from the icon height — if the label
  overlaps the icon, check that `CityLayer` passes `dotRadius={iconSize}` to
  `CityMarkers`.
- For clustered cities, alternate positions so labels don't stack.

## Region labels — visibility fade, not opacity dimming

Earlier versions used semi-transparent region labels that looked pink on
warm terrain. Current rule: binary visibility via distance to viewport edge
with a 20px soft fade band. If you add regions, trust the existing
`RegionLabelsLayer` — do not introduce new opacity fades.

Do NOT re-enable `BoundariesLayer` with offline projection — it drifts on
moving cameras. Shelved.

## Performance

- Render overlays on chroma-key magenta (`#FF00FF`) as JPEG, then composite
  over the Cesium MP4 with ffmpeg `colorkey`. ~3× faster than PNG+alpha.
- Use `h264_videotoolbox` for final encode on this Mac.
- Never `<Video>`-decode the Cesium MP4 inside Remotion for final output —
  the decode tax kills render speed. Composite in ffmpeg.

## Color palette (parchment aesthetic)

- Ink / strokes: `#2A1208`
- Gold / fill accent: `#C4903A`
- Highlight red (routes, fires): `#8B1A1A`
- Shadow: `#5b3a14`
- Parchment (flat, no gradient — gradients drift pink under blend modes):
  `#d9c085`

These are locked to match the icon set. Don't introduce new accents without
checking the full scene — warm-on-warm blends drift pink fast.

## How to tell a new story on this engine

1. **Pick the path.** Stylized for symbolic moments, Cesium for real terrain.
2. **Pick or record a camera flight.** If Cesium, use `globe-plugin/` to
   record a new MP4 + trajectory pair. Reuse existing ones where possible.
3. **Write the config JSON.** `durationInFrames`, markers, cityMeta with the
   right icon types, reveal frames, label positions, routes, fireTiming.
4. **Register in `src/Root.tsx`.** Mirror an existing entry.
5. **Typecheck:** `npx tsc --noEmit` before rendering.
6. **Render a still first:** `npx remotion still <Id> out/preview.png
   --frame=<midpoint>` to sanity-check icons+labels don't collide.
7. **Render video:** `npx remotion render <Id> out/<name>.mp4`. Or use the
   two-pass overlay+composite pipeline if it's a Cesium composition.

## Always check before shipping

- Every label clears its icon at every reveal frame.
- No pink drift in background regions.
- Route arrows terminate AT the icon base (not floating next to it).
- City reveal timing matches narration (if known).
- ffmpeg composite output has no green/magenta fringes at icon edges.

## Message bus (if collaborating with Claude Design)

Drop-off: `inbox/design/`. Pickup: `inbox/code/`. Assets: `assets/`.
One message = one file = one commit. See `README.md` in this repo for the
full protocol.
