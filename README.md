# Eclipse Descent — Alpine Totality Ski

A single-file, hyperrealistic-feel ski experience built around one idea: **carve a high
alpine face while the moon swallows the sun.** The sibling of the Iceland / Egypt eclipse
*flight* sims — same house style, different verb.

One `index.html`, Three.js (r128) from a pinned CDN, no build step. Open it, or drop the
folder on any static host.

## Two ways down the mountain (menu)

- **Free Ride** — endless roam, the Iceland-flight-sim way: the eclipse runs on its own
  real-time clock (~90 s to totality, hold, release, repeat — `E` fast-forwards). Cross the
  base and you wrap back to the summit for another lap. Carve, catch air, clip gates.
- **Adventure** — the same mountain as a challenge run, in three difficulties:
  - **Green · easy** — 5 hearts, sparse snowballs, wide target
  - **Blue · steeper** — 4 hearts, faster & more obstacles, medium target
  - **Black · expert** — 3 hearts, fast dense snowballs, narrow target

  **Dodge** the rock outcrops and the rolling **snowballs** (each hit costs a heart; run out and you
  wipe out), then hit the big final kicker and **stick the landing on the bullseye target**
  to complete the run. Tuned to be a real challenge without being punishing — hits give you
  a short invulnerability window, and the target is generous on Green.

Terrain look referenced from **Cardrona / Treble Cone (NZ)** — treeless high-country bowls,
golden tussock and scree bleeding through the snow, rock bands along the apron.

## The eclipse (both modes)

A single `phase` (0 → 1) — time-driven in Free Ride, descent-driven in Adventure — couples lights, fog, the sky shader, the sun/moon/corona, stars, snow tint,
and bloom in lockstep: brilliant daylight at the summit → partial → diamond ring →
**totality at the valley floor**, corona blooming dead ahead as you carve toward it.

## Controls

| | |
|---|---|
| `← →` | carve |
| `↑` / `space` | tuck (speed) |
| `↓` | check speed (hockey stop) |
| `E` | hasten the eclipse |
| `R` | restart run · `M` | menu |
| mouse / touch | drag to steer, hold to tuck (mobile has a TUCK button) |
| 🔊 | sound on / off |

## Craft notes

- **Procedural sound engine** (WebAudio, zero asset files): continuous ski-carve swish
  (volume/pitch track speed & edge angle), wind, jump/land thuds, impact hits, gate dings,
  a low totality drone that swells toward darkness, and success / fail / bullseye chimes.
- **Realism pass:** ACES filmic tone mapping, real-time sun shadows, real CC0 PBR snow textures (color/normal/roughness from ambientCG), a crisp canvas-drawn eclipse (visible moon bite all run + streamer corona at totality), distant ridge silhouettes with aerial haze, soft round snowflakes + drifting snowfall, volumetric powder
  spray off the edges, persistent carve tracks, a phase-driven bloom on the corona and
  glints (desktop; auto-off on low-power devices), FOV widening and a subtle camera bob at
  speed.
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
