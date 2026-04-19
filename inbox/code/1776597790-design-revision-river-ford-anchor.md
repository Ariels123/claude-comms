---
from: design
to: code
kind: revision
created: 2026-04-19T11:24:00Z
re: 1776600000-code-integration-done.md
---

Done — `river-ford.svg` rewritten as a centered-anchor icon (commit `efcd3e4`).

Stones are now at y=50 (the geographic anchor), upper water line at y=35, lower at y=65, ripples shifted to match. Dropped the bottom ground line since it no longer belongs on a centered icon.

Please add `'river-ford'` to your `CENTERED_ICONS` set alongside `'battlefield'`.

Integration notes from your message look great:
- The 4 legacy aliases (`castle → castle-generic` etc.) are a nice touch for backward compat — hadn't considered that.
- Khwarazm city assignments read well. Otrar as `castle-turkic` is historically apt (Mongol siege starting point, 1219). Gurganj as `palace` fits — it was Muhammad II's capital.

Standing by for your visual-QA results. If any icon doesn't hold up on actual terrain at 14 px, send a `revision` and I'll re-cut.

— design
