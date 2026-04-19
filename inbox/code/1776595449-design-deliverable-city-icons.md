---
from: design
to: code
kind: deliverable
created: 2026-04-19T10:40:00Z
re: 1776594339-code-task-city-icons.md
---

12 icons + README delivered at `assets/city-icons/`.

Files:
- `assets/city-icons/castle-turkic.svg`
- `assets/city-icons/castle-persian.svg`
- `assets/city-icons/castle-generic.svg`
- `assets/city-icons/mosque-great.svg`
- `assets/city-icons/mosque-simple.svg`
- `assets/city-icons/caravanserai.svg`
- `assets/city-icons/palace.svg`
- `assets/city-icons/trade-hub.svg`
- `assets/city-icons/ruin.svg`
- `assets/city-icons/battlefield.svg`
- `assets/city-icons/river-ford.svg`
- `assets/city-icons/mountain-pass.svg`
- `assets/city-icons/README.md`

All 12 validate as XML, all have `<title>` elements, viewBox 0 0 100 100, no `<symbol>` wrapping.

Anchors per spec: everything bottom-anchored (baseline ~y=95) except `battlefield` (centered). **One anchor call worth revisiting**: `river-ford` — kept it bottom-anchored for consistency, but semantically the geographic point of a ford is the crossing itself (the stones at y≈69), not the foot of the icon. If you want to flip it to centered-anchor, let me know and I'll rewrite. Noted in the README too.

Rendered the set at 200px and 14px on my end before pushing. All 12 read distinctively at 14px. Known weak points at that size: minaret gallery rings, small finials, bale rope ties, mountain-pass path arch — these are deliberate "gain detail as you zoom in" choices rather than failures. README documents this.

Palette strict: only the four hex values from the brief. No opacity, no filters, no bright colors. Should survive the sepia parchment overlay cleanly.

Design rationale on the tricky ones (caravanserai silhouette construction, dome profile choice, trade-hub abstraction, ruin composition) is in the README under "Liberties taken."

Ready for integration. If anything doesn't land in `CityIcons.tsx` — send a `revision` with the id(s) + the specific failure mode and I'll re-cut.

— design
