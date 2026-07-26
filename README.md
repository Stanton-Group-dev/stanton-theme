# @stanton/theme

Stanton fleet design tokens, distributed as a git-tagged npm dependency — **no npm
registry involved**. One versioned source replaces the per-repo hand-copies of
`theme-internal.css` / `theme-external.css`.

**Spec of record:** `stanton-control/standards/ui-standard.md` (§2.1 internal, §2.2
external, §9 motion). This repo is the *code* source of truth for token values; the
standard is the *specification* (measured contrast ratios, usage rules, governance).
Token changes require Alex's §8 sign-off there before they land here.

## Consuming

```jsonc
// package.json
"dependencies": {
  "@stanton/theme": "github:Stanton-Group-dev/stanton-theme#v1.0.0"
}
```

```css
/* app entry css — pick the register(s) the app hosts */
@import "@stanton/theme/theme-internal.css";
```

Pick up a fleet-wide token change with `npm update @stanton/theme` after bumping the
pinned tag. **Never fork these files locally** — gaps route upstream as change
requests, the same rule the copy model always had, now enforced by the dependency
boundary.

## Contents

- `theme-internal.css` — internal register ("Cold Luxury"), staff surfaces.
  Selector: `:root[data-stanton-register="internal"]`.
- `theme-external.css` — external register ("Stanton paper"), tenant / prospect /
  contractor surfaces. Selector: `:root[data-stanton-register="external"]`.

Both are pure CSS custom properties — framework-agnostic across the fleet's stack
split (Tailwind v3/v4, React 18/19, Next/Vite).

## Releasing

1. Land the token change here (after §8 sign-off in ui-standard.md).
2. Bump `version` in package.json, commit, tag: `git tag vX.Y.Z && git push --tags`.
3. Never move or delete an existing tag — apps pin to tags and must never see one
   change value under them. Walk a bad release back with a new patch tag.
4. Keep `stanton-control/templates/ui/theme-*.css` in sync (human-readable spec
   mirror) until §8 rules otherwise.
