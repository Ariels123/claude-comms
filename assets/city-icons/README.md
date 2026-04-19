# City icons — Khwarazmian Empire map set

12 SVG icons for rendering on sepia-parchment-filtered satellite imagery, narrating the Mongol invasion of 1218–1223 CE. Designed for 14–24 px render in a `<symbol>`-based engine.

Files are plain, un-minified, each starts directly with `<svg>` (no XML declaration, no `<symbol>` wrapping — per brief), each has a `<title>` for accessibility. 100×100 viewBox throughout.

## Icons

| id | description | anchor |
|---|---|---|
| `castle-turkic` | Steppe-style fortified tower. Battered (outward-sloping) walls with two asymmetric merlons and an arched gate. | bottom |
| `castle-persian` | Tall narrow tower with a central conical cap, finial ball, and an arrow-slit on the face. | bottom |
| `castle-generic` | Neutral fortified town — symmetric crenellated rectangle (three merlons) with an arched gate. | bottom |
| `mosque-great` | Large central pointed dome + drum, flanked by two slender Kalyan-type minarets with gallery rings. | bottom |
| `mosque-simple` | Small pointed dome centered on a square base, with one squat minaret attached to the base's right edge. | bottom |
| `caravanserai` | Wide continuous wall with corner turrets and a dominant raised central pishtaq framing the arched gate. | bottom |
| `palace` | Three stepped tiers with a large central iwan and a small crowning dome + finial. | bottom |
| `trade-hub` | Abstract bale of goods, cinched with a cross-rope and a central knot. | bottom |
| `ruin` | Castle-generic silhouette with an asymmetrically collapsed top — left side retains merlons, right side crumbles — plus rubble dots at the base. | bottom |
| `battlefield` | Crossed saber (curved, lower-left to upper-right) and spear (straight, upper-left to lower-right) forming an X, with a small red pennant fluttering from the cross-point. | **center** |
| `river-ford` | Two wavy water lines with three stepping-stones across. | bottom (see note) |
| `mountain-pass` | Two asymmetric peaks (taller left, shorter right) with a visible notch between them and a subtle arched path suggestion through the pass. | bottom |

## Liberties taken

A running list of design decisions where I interpreted the brief rather than followed it literally. If any of these don't match the vision, send a `revision` message with specifics.

- **Turkic vs. Persian silhouette.** I leaned on architectural cues beyond crenellation alone. The Turkic castle has *battered* (trapezoidal, slightly outward-splaying) walls — a steppe fortification convention — while the Persian castle is vertical-walled with a conical/finial-topped tower, referencing Khorasanian tower architecture (Gunbad-e Qabus, Radkan East). At 14 px the two still read as distinct: squat-and-flared vs. tall-and-pointed.
- **Dome shape.** Went with a moderately pointed / slight-onion profile rather than a shallow Kalyan-era hemisphere, because at 14 px a shallower dome reads as a generic "bump" rather than an Islamic religious structure. The pointed dome carries the cue more reliably at small sizes. If you want the flatter historical profile, it's a one-line fix per affected icon.
- **Caravanserai pishtaq as single silhouette.** The wall + corner turrets + raised central pishtaq are drawn as one continuous outline path rather than stacked separate rectangles. This keeps the silhouette clean (no overlapping internal strokes) and makes the pishtaq's vertical prominence read clearly — which is the defining iconographic feature of Central Asian caravanserais (Ribat-i Sharaf, Sultan Hanı).
- **Palace iwan.** Three stepped masses + a central iwan (tall arched opening) + a small crowning dome. The stepped silhouette is what differentiates this from a mosque — otherwise "palace with dome" and "mosque-simple" would look interchangeable at 14 px.
- **Trade-hub choice.** Chose the abstract bale over a packed-camel silhouette. At 14 px a camel becomes an indistinct blob; a trapezoidal bundle with a visible cross-rope knot reads much more robustly and has a nice marginalia flourish. If you'd prefer the camel variant, I can cut a `-alt`.
- **Ruin left-intact composition.** Kept the left third of the wall with recognizable merlons so that at small sizes the viewer reads "this was a castle" rather than "this is a jagged hill." The right side fully crumbles. Rubble dots at the base reinforce the reading.
- **Battlefield red pennant.** Per the palette's "red, use sparingly (banner fields)" note, the small red pennant sits at the X's cross-point rather than a full rectangular flag on a pole. Keeps the crossed-weapons X as the dominant silhouette while honoring the "on a banner" brief. Centered anchor per spec.
- **River-ford anchor.** Spec lists battlefield as *the* example centered variant, so I've kept river-ford bottom-anchored for consistency. However: a ford semantically represents the geographic point at the water crossing, which visually sits in the middle of this icon (the stones, at y≈69), not at its foot. If the map engine places the icon so the geographic point aligns with the icon's bottom, the ford's visual "location" will appear ~25 units above the true point. **Flagging this as a candidate for center-anchoring** — cheap fix (rewrite path y-coords) if you want me to switch it.
- **Mountain-pass path.** Added a small arched line in the notch between peaks — a visible suggestion of *the path through the pass*. Subtle at 14 px, meaningful at 20+. Helps distinguish this icon from generic "two mountains."
- **Stroke weights.** Used 2.0 px (top of the specified range) as the default for main outlines, 2.4–2.6 px for baseline "ground" lines on bottom-anchored icons (implies terrain without adding a separate element), and 1.2–1.5 px for interior detail strokes (ripples, finial stems, the pass path). Spear shaft is 2.5 px, saber blade is 3 px — weapons want to feel heavier than architecture.

## Palette usage

| color | hex | used on |
|---|---|---|
| ink / primary stroke | `#2A1208` | all silhouette outlines, gate cut-ins (filled), weapon shafts, baselines, arrow slits |
| gold / fill | `#C4903A` | main body silhouettes, stepping stones, bale, mountain peaks, minaret caps, knot |
| blood red | `#8B1A1A` | battlefield pennant only |
| shadow / secondary | `#5b3a14` | minaret gallery rings, snow caps, secondary water ripples, dome finial balls, weapon pommels, rubble dots, river-ford baseline |

No `opacity`, no `filter`, no non-palette colors used anywhere. All shapes should survive the sepia overlay cleanly — gold carries the silhouette, ink carries the outline, the two together read across zoom levels.

## Known trade-offs at 14 px

What survives cleanly: silhouettes, dome and peak profiles, the X of the battlefield, the crenellation step pattern, the wavy river lines.

What weakens or merges at 14 px: minaret gallery rings (become smudges), small finials (become dots), the tamga-style accents and internal window slits, rope lines on the bale, the mountain-pass path arch, the pennant's fluttering edge detail.

That's a deliberate choice — bold legible shape at small sizes, richer detail as the map zooms. Each icon should *gain* information as it grows, not be redundant at 24 px.

If anything doesn't land in the `CityIcons.tsx` integration, send a `revision` message naming the id(s) and the specific failure mode (doesn't read, wrong reading, clashes with another icon, etc.) and I'll re-cut.

— design
