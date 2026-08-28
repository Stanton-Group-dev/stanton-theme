---
repo: stanton-theme
updated_at: 2026-08-27
scanned_at: 2026-08-27
head_sha: 22cb3e28778a913406b1595f4cb6542fd35f03f0
source: hand
generated: false
ttl_days: 90
action_surfaces:
  - "theme-internal.css"
  - "theme-external.css"
  - "package.json"
---

## Internal register token set ("Cold Luxury")
- type: integration
- status: shipped
- invoke: `@import "@stanton/theme/theme-internal.css";` then set `data-stanton-register="internal"` on `:root` or a wrapper element
- verified: unverified
- verified_at: null
- files: [theme-internal.css]
- hints: [readonly]
- notes: Pure CSS custom-property set for staff/internal surfaces — no build step, no JS. Selector matches both `:root[data-stanton-register="internal"]` and the bare-attribute form (v1.1.0 widening) so apps hosting both registers under one `<html>` can mount the marker on a wrapper instead of `:root`. Covers surface/border colors, text colors, a closed semantic set (accent/success/destructive/warning, sign-off gated per ui-standard.md §2.1), radii, spacing scale, type tokens (Geist self-hosted font stack), and a shared motion vocabulary (durations/easings). Spec of record and contrast measurements live in `stanton-control/standards/ui-standard.md` §2.1 — this repo is the code source of truth, not the spec.

## External register token set ("Stanton paper")
- type: integration
- status: shipped
- invoke: `@import "@stanton/theme/theme-external.css";` then set `data-stanton-register="external"` on `:root` or a wrapper element
- verified: unverified
- verified_at: null
- files: [theme-external.css]
- hints: [readonly]
- notes: Pure CSS custom-property set for tenant/prospect/contractor surfaces — square corners, serif reserved for wordmark/title, gold accent restricted to rules and step marks (never text/fills, decorative-only by measured contrast). Same v1.1.0 wrapper-hosted-register selector widening as the internal set. Covers surfaces, text, a closed semantic set (primary/success/destructive/warning, sign-off gated per ui-standard.md §2.2), spacing, a 44px minimum touch target, serif+sans type tokens (Libre Baskerville + Inter, self-hosted), and the same shared motion vocabulary as the internal register. Spec of record: `stanton-control/standards/ui-standard.md` §2.2.

## Distribution / versioning mechanism
- type: integration
- status: shipped
- invoke: consumers pin `"@stanton/theme": "github:Stanton-Group-dev/stanton-theme#vX.Y.Z"` in package.json `dependencies`; `npm update @stanton/theme` after bumping the pinned tag picks up a fleet-wide token change
- verified: unverified
- verified_at: null
- files: [package.json, README.md]
- notes: No npm registry involved — distributed as a git-tagged dependency (`files` field in package.json whitelists only the two CSS files). No build step, no `exports`/`main` entry point, no JS at all. Releasing is a manual protocol (README "Releasing" section): land the sign-off'd token change, bump `version`, commit, tag `vX.Y.Z`, never move/delete an existing tag (walk back with a new patch tag instead), and keep `stanton-control/templates/ui/theme-*.css` in sync as a human-readable mirror. Current version at HEAD: 1.1.0.
