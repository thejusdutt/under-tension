# UNDER TENSION

**Live: https://under-tension.pages.dev**

A single-file home hypertrophy reference — 18 movements across 6 muscle groups,
ranked best-first, for adjustable dumbbells (≤ 30 kg) + bodyweight. Built to be
glanced at mid-session on a phone: each exercise has a looping **3D-animated
figure** that performs the actual rep — slow eccentric, a held, glowing pause at
the stretched position (the growth-relevant part), then the concentric.

## How it works

Everything lives in one `index.html` — no build step, no frameworks, no external
dependencies except Google Fonts.

- **3D figures**: a tiny software-rendered 3D engine on `<canvas>`. Each exercise
  is defined as 3D joint keyframes (top pose + stretch pose), interpolated with
  bone-length re-normalization, perspective-projected with depth shading, tapered
  volumetric limbs, a slow camera orbit, and a ground shadow.
- **Stretch emphasis**: ~22% of every rep cycle is a held stretch with a violet
  glow at the working muscle; dashed trails trace the hand/bar path.
- **Interaction**: sticky segmented nav (bottom thumb-bar on phones), one
  expandable card at a time with cues and dose, and an in-memory set timer with a
  90 s rest countdown. No localStorage, no forms.
- **Accessibility**: semantic HTML, visible focus, and `prefers-reduced-motion`
  freezes every figure at its stretched position (statically informative, not blank).
- Exercise selection and the global rules follow longitudinal hypertrophy
  trials, not EMG — references are footnoted on the page.

## Deploy

Hosted on Cloudflare Pages:

```sh
npx wrangler pages deploy . --project-name=under-tension
```
