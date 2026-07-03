# Eclipse Descent — Alpine Totality Ski

A single-file, hyperrealistic-feel ski experience built around one idea: **carve a high
alpine face while the moon swallows the sun.** The sibling of the Iceland / Egypt eclipse
*flight* sims — same house style, different verb.

One `index.html`, Three.js (r128) from a pinned CDN, no build step. Open it, or drop the
folder on any static host.

## Two ways down the mountain (menu)

- **Free Ride** — endless roam, the Iceland-flight-sim way: the eclipse runs on its own
  real-time clock (`E` fast-forwards). Cross the base and you wrap back to the summit for
  another lap. Carve, catch air, clip gates.
- **Adventure** — the same mountain as a challenge run, in three difficulties:
  - **Green · easy** — 5 hearts, sparse snowballs, wide target
  - **Blue · steeper** — 4 hearts, faster & more obstacles, medium target
  - **Black · expert** — 3 hearts, fast dense snowballs, narrow target

  **Dodge** the rock outcrops and the rolling **snowballs** (jump to clear them) — plough into a rock
  and you stop dead and get stuck; mash jump to dig yourself out early, or wait it out. Each hit costs
  a heart, and if you run out you wipe out. Then hit the big final kicker and **stick the landing on
  the bullseye target** to complete the run. Tuned to be a real challenge without being punishing —
  hits give you a short invulnerability window, and the target is generous on Green.

Terrain look referenced from **Cardrona / Treble Cone (NZ)** — treeless high-country bowls,
golden tussock and scree bleeding through the snow, rock bands along the apron.

## The eclipse (both modes)

One shared real-time clock drives the identical eclipse in **both** modes — Adventure is the
same world with obstacles layered on. The cycle: the moon takes its bite fast (**30 s** to a
deep partial), eases slowly into totality over another **30 s**, **holds totality for 45 s**
(long enough to ride inside it), releases over **30 s**, then loops. A single `phase` (0 → 1)
couples lights, fog, the sky shader, the sun/moon/corona, stars, snow tint, and bloom in
lockstep: brilliant daylight → partial → diamond ring → **totality** → release.

## Controls

| | |
|---|---|
| `← →` | carve |
| `↑` / `W` | tuck (speed) |
| `space` / `K` | jump (hop over rocks & snowballs) |
| `↓` | check speed (hockey stop) |
| `E` | hasten the eclipse |
| `R` | restart run · `M` | menu |
| mouse / touch | drag to steer, hold to tuck; mobile has TUCK + JUMP buttons |
| 🔊 | sound on / off |

## Craft notes

- **Procedural sound engine** (WebAudio, zero asset files): continuous ski-carve swish
  (volume/pitch track speed & edge angle), wind, jump/land thuds, impact hits, gate dings,
  a low totality drone that swells toward darkness, and success / fail / bullseye chimes.
- **Realism pass:** ACES filmic tone mapping, real-time sun shadows, real CC0 PBR snow textures (color/normal/roughness from ambientCG), a crisp canvas-drawn eclipse (visible moon bite all run + streamer corona at totality), distant ridge silhouettes with aerial haze, soft round snowflakes + drifting snowfall, volumetric powder
  spray off the edges, persistent carve tracks, a phase-driven bloom on the corona and
  glints (desktop; auto-off on low-power devices), FOV widening and a subtle camera bob at
  speed.
- **Majestic eclipse sky** — a 360° twilight ring glowing all around the horizon (warm at
  the base, rose then deep-violet to the zenith, brightest toward the hidden sun), the
  Milky Way arcing overhead in procedural nebulosity, a two-layer coloured starfield,
  planets (Venus/Jupiter/Mars) emerging, a black moon disc ringed by a pearly corona with
  chromosphere and red prominences, and a diamond-ring flare on the limb at the edges of
  totality.
- **One driver, whole mood** — `applyEclipse(phase)` couples everything to a single number.
- **Single-source terrain** — `heightAt(x,z)` builds the mesh *and* resolves collision,
  moguls, valley walls, and every kicker lip, so the skier can never disagree with the
  ground.
- **Self-contained & mobile-solid** — instanced pines & snowballs, capped
  `devicePixelRatio`, `dt` clamp, debounced resize, rAF paused when hidden, touch controls,
  procedural fallbacks everywhere. No blank screen.

## Deploy

Static single file. Drag the folder to Netlify, or git-connect a repo and push. No build
command; publish directory is the repo root.
