# Reading Room — showcase site

A small, self-contained marketing/showcase site for the Reading Room app. It is **not**
part of the app build — this folder is gitignored in the ReadingRoom repo and is **its own
git repository** now (private for the moment; it will become the GitHub Pages site).

## Pages
- `index.html` — Home (overview, features, screenshots, the Analyze GIF).
- `how-to-use.html` — step-by-step walkthrough with screenshots + GIFs, framed around the app.
- `how-to-install.html` — get the files (clone / ZIP), prerequisites, launching the app, first run.

## Assets
- `assets/site.css` — styles; mirrors the app's design tokens (Fraunces / Inter / JetBrains Mono, indigo accent, light+dark).
- `assets/logo.png` — the constellation logo (copy of `assets/reading-room-logo.png`).
- `assets/shots/*.png` — screenshots captured from the running app
  (`catalogue`, `catalogue-list`, `report`, `graph`, `library`, `setup`), at 2× for retina.
- `assets/shots/*.gif` — the Analyze flow (`analyze.gif`) and the app tour (`apptour.gif`).
- All screenshots and GIFs are **copied from the app repo's `assets/shots/`** — re-capture there, then copy them here.

## Notes
- Pure static HTML/CSS — no build step, no dependencies. Open `index.html` directly, or serve the folder.
- Fonts load from Google Fonts (same as the app); everything else is local.
- Light/dark toggle persists under the `rr-site-theme` localStorage key (separate from the app's `rr-theme`).
- Wording: it's "Reading Room" / "the app" everywhere — never "work mode" (that's the internal folder name).
- `.video-ph` blocks hold the GIFs; swap in a `<video>`/embed if you record something longer.

## To re-capture screenshots
Use the agent driver from the ReadingRoom repo root — it launches the app headless (no window), waits
for the page to settle, and screenshots it at a **1200×800 viewport rendered at 2×** (a 2400×1600 PNG):

```
node .claude/skills/run-reading-room/driver.mjs shot /           website/assets/shots/catalogue.png
node .claude/skills/run-reading-room/driver.mjs shot graph.html  website/assets/shots/graph.png 8000
```
(`shot <page|url> <out.png> [waitMs]` — repeat for the report / library / setup pages; the
connections graph needs the longer wait for the force layout to settle. Override the viewport
with the environment variables `RR_SHOT_W`, `RR_SHOT_H`, and `RR_SHOT_SCALE` — e.g.
`RR_SHOT_SCALE=1` for a 1× capture. The driver closes the tutorial and setup modals first.)

## Inserting into your personal site
Copy this folder (e.g. as `reading-room/`) into your site and link to it. If your site
already defines `--bg`, `--ink`, etc., scope these styles or rename the tokens to avoid
collisions; otherwise it's drop-in.
