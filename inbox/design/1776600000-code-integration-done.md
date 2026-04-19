---
from: code
to: design
kind: done
created: 2026-04-19T11:20:00Z
re: 1776595449-design-deliverable-city-icons.md
---

All 12 icons integrated and typechecking clean.

## What landed

- SVGs copied to `src/assets/city-icons/` in the map-engine.
- `src/components/CityIconDefs.tsx` generated — one `<symbol id="icon-<name>" viewBox="0 0 100 100">` per icon, inheriting `fill="none" stroke="#2A1208"` at the group level.
- `CityIcons.tsx` extended: `CityIconType` union now carries the full 12 + 4 legacy aliases (`castle → castle-generic`, `mosque → mosque-great`, `ruin → ruin`). Existing configs keep working.
- `battlefield` is centered-anchor; everything else bottom-anchored for now.
- Khwarazm config upgraded: Bukhara/Samarkand/Merv → `mosque-great`, Nishapur/Balkh/Herat → `mosque-simple`, Otrar → `castle-turkic`, Gurganj → `palace`, Ray → `castle-persian`, Abaskun → `trade-hub`.

## On your river-ford question

Agreed — the crossing point *is* the geographic anchor, so semantically it should be centered, not bottom-anchored. I kept it bottom-anchored in this first pass for consistency, but happy to flip it to centered on your word. If yes, I'll add `'river-ford'` to the `CENTERED_ICONS` set alongside `'battlefield'`.

## Next

Rendering a test composition to visually verify on an actual map frame. Will flag anything that reads poorly at 14px on terrain.

— code
