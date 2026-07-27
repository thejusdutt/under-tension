# UNDER TENSION

**Live: https://under-tension.pages.dev**

A single-file home hypertrophy reference — 18 movements across 6 muscle groups,
ranked best-first, for adjustable dumbbells (≤ 30 kg) + bodyweight. Built to be
glanced at mid-session on a phone: each exercise has a looping **3D-animated
figure** that performs the actual rep — slow eccentric, a held, glowing pause at
the stretched position (the growth-relevant part), then the concentric.

**Every figure holds still until you play it.** Until then each one sits in its
stretched position — the frame worth looking at — behind a play badge. Tapping a
figure runs that one set; tapping another hands over to it, so exactly one figure
animates at a time and an idle page schedules no frames at all.

## How it works

Everything lives in one `index.html` — no build step, no frameworks, no external
dependencies except Google Fonts.

- **3D figures**: a tiny software-rendered 3D engine on `<canvas>`. Each exercise
  is defined as 3D joint keyframes (top pose + stretch pose). Bones keep their
  authored length and swing by **slerp**, so joints rotate at constant angular
  velocity instead of sliding between poses.
- **Body mechanics**: the trunk is not one rigid slab. A derived mid-spine joint
  **arches** toward the front of the body — the ribcage lifting off the pad on a
  bench, the low back staying long at the bottom of an RDL, the hips sagging in a
  plank — and the torso outline runs shoulder → waist → hip so the silhouette bows
  with it. The **shoulder girdle** slides over the ribcage where that is the point
  of the lift (full protraction at the bottom of a row, pinned back on a bench).
  Late in a hard set a standing lifter stops being strict: the knees **dip and
  drive** and the back extends into the rep. The direction "forward" is derived
  per pose from the shoulder line and the spine, so the same code is correct lying
  on a bench, hinged over, or upright, and no pose has to declare which way it faces.
- **Rep mechanics**: every phase is integrated from a **velocity profile** rather
  than written as a position curve, and each profile eases to zero at both ends,
  so position *and* speed stay continuous across all four joins — the movement
  never snaps from a standstill to full speed. A rep eases off lockout, lowers at
  a steady rate, decelerates a long way into the stretch, holds, drives out of the
  bottom, **grinds** through a sticking region, and decelerates into lockout. The
  sticking region scales the drive down instead of being subtracted from it, so a
  hard rep grinds (2.2× slower on rep 1, 3.8× by rep 6) but never stalls. Each
  figure runs a **set of six**, not one perfect rep on loop: across the set the
  reps lengthen, the grind deepens, the tremor grows, the range shortens slightly.
- **Life on top of the rig**: breathing lifts the ribcage along the spine and the
  shoulder girdle rides it, the loaded arm oscillates about the shoulder at
  ~1.5 Hz with a finer ~7 Hz tremor on top, the body sways over planted feet, and
  a flexed elbow or knee bunches the muscle it's working. All of it is applied as
  **rigid rotation**, so bones keep their length exactly, and all of it scales
  with how hard the current instant of the rep is — the lockout is dead still,
  the sticking point of the last rep is the worst of it. Hands planted on a floor
  or a bar do not wobble.
- **Look**: key-lit capsule limbs with a dark contour so overlapping limbs read
  apart, a rounded tapered torso, dumbbell plates as real cylinders, contact
  shadows that widen and fade the further a joint is off the floor, a slow
  non-uniform camera orbit, and a violet comet on the path the load just covered.
- **Stretch emphasis**: ~19% of every rep cycle is a held stretch with a violet
  glow at the working muscle; dashed trails trace the hand/bar path.
- **Interaction**: a play/pause button over each figure, sticky segmented nav
  (bottom thumb-bar on phones), one expandable card at a time with cues and dose,
  and an in-memory set timer with a 90 s rest countdown. No localStorage, no forms.
- **Accessibility**: semantic HTML, visible focus, playback is a real `<button>`
  with `aria-pressed` (so it works from the keyboard and reads correctly to a
  screen reader), and `prefers-reduced-motion` never starts the figures at all —
  they stay frozen at the stretched position (statically informative, not blank),
  and no play button is rendered for a figure that cannot animate.
- Exercise selection and the global rules follow longitudinal hypertrophy
  trials, not EMG — references are footnoted on the page.

## Deploy

Hosted on Cloudflare Pages:

```sh
npx wrangler pages deploy . --project-name=under-tension
```
