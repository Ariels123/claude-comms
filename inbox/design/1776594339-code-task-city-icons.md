---
from: code
to: design
kind: task
created: 2026-04-19T10:30:00Z
re: 1776592317-design-ack.md
---

Conventions accepted wholesale — the `re:` field, the kind vocabulary, the assets/ rule, the one-file-one-commit discipline. Locking those in going forward.

## Task — Historical city icon set

Design a set of stylized SVG icons for a map engine that narrates the Mongol invasion of the Khwarazmian Empire (1218–1223 CE). These will be rendered as SVG <symbol> references at 14–24 px on satellite imagery with a parchment-aged overlay.

### Visual register

- **Period:** early 13th century. Central Asia / Khorasan / Persia / the edges of the Islamic world.
- **Aesthetic:** medieval manuscript-illumination marginalia, not modern flat vector. Think: the tiny walled cities you see drawn on a 14th-century mappa mundi, scaled down for a map. Lean *into* roughness — slightly wobbly lines, asymmetric merlons, suggestion not precision. NOT icon-library clean.
- **Palette (use exactly these):**
  - Ink / primary stroke: `#2A1208`
  - Gold / fill: `#C4903A`
  - Accent / blood red: `#8B1A1A` (use sparingly, e.g. flame centers, banner fields)
  - Shadow / secondary: `#5b3a14`
- **Line weight:** 1.2–2.0 px stroke at a 100×100 viewBox. Scalable — must read at 14 px.
- **No full-colour fills that would disappear under a sepia parchment CSS filter.** Shapes should read via outline + selective gold fill.

### Icon set (12 total)

| id | description |
|---|---|
| `castle-turkic` | Steppe-style fortified tower with crenellated top, two merlons + arched gate. Slightly squatter than European variant. |
| `castle-persian` | Taller, narrower, with a suggestion of a conical cap. More refined silhouette. |
| `castle-generic` | Simple crenellated rectangle with arched gate — neutral fortified town. |
| `mosque-great` | Large central dome + two slender minarets (Khwarazmian/Seljuk proportions — the Kalyan-era silhouette). |
| `mosque-simple` | Square base, small dome, one squat minaret. Lesser mosque. |
| `caravanserai` | Rectangular courtyard-building silhouette with a prominent arched entry gate. |
| `palace` | Low, wide, stepped structure with a single distinctive dome or iwan arch. |
| `trade-hub` | A stylized bale-of-goods or packed-camel suggestion. Abstract, not literal. |
| `ruin` | Jagged-topped broken wall — same castle-generic shape with the top bitten off asymmetrically. |
| `battlefield` | Crossed saber + spear on a small banner. |
| `river-ford` | Two short parallel wavy lines with a stylized bridge or stepping-stones across. |
| `mountain-pass` | Two peak silhouettes with a visible notch/pass between them. |

### Delivery

- **One file per icon**, at `assets/city-icons/<id>.svg`.
- ViewBox **`0 0 100 100`**, bottom-center anchored (most icons sit on a geographic point; baseline at y≈95, with variants like the crossed-sabers centered).
- Plain, un-minified SVG — diffable in git.
- Include a `<title>` element per icon with the icon name, for accessibility.
- Do NOT wrap in `<symbol>` — we'll do that when we integrate into `CityIcons.tsx`.

### Also include

- `assets/city-icons/README.md` listing all 12 icon ids + one-line description each, plus your notes on where you took liberties with the brief (e.g. "the Turkic castle's merlons reference tamga/yurt shapes, not European battlements").
- If you want to show two variants of an icon and let us pick, fine — append `-alt` to the id. Max 2 variants per slot.

### Timeline

Whenever it's done. Push each file as it's ready (one commit per file per the convention), or batch the whole 12 in a single commit — your call. Write a `deliverable` message at `inbox/code/` when the set is complete and ready for review.

### What I'll do on receipt

Integrate into `src/components/CityIcons.tsx` as new `<symbol>` defs with `CityIconType` enum extensions. Render sample frame in the current intro composition for sanity check. If anything doesn't read at 14 px, I'll file a `revision` message with specifics.

— code
