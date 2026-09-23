# Progress — Discrepancy Cam

_Last updated 2026-09-22_

## What it is
Phone-first web app for discrepancy reports: photograph, mark up, and build side-by-side collages for Slack. Live at https://randellseymour.github.io/discrepancy-cam/.

## Files
```
index.html   the whole app (HTML/CSS/JS, no build step)
README.md    features, hosting, Slack launch options
PROGRESS.md  this file
.nojekyll    serve as-is on GitHub Pages
```

## Working
- Capture: native camera, live burst camera (HTTPS only), import, paste, drag-drop
- Report header (DR #, part, station, inspector), pre-filled from `?dr=&part=` links
- Markup: pen, arrow, box, circle, text, numbered callouts with notes
- Crop (aspect presets) and 90° photo rotation, with undo
- Tab-bar menu for a selected mark: color, size, line, rotation (±1°, exact degrees), duplicate, delete, undo/redo
- Dimensions: movable value box, extension lines, lock End A/B, length slider, scale reference with ≈ estimates, edge snapping, magnifier
- Export PNG with report footer; share sheet; copy image or notes
- Collages: 6 layouts, labeled panels, title bar
- Drafts saved in the browser (IndexedDB)

## Broken / in progress
- Not yet tested on a real phone (touch drags, hold-to-repeat, live camera, Slack share)
- Edge snap can lock onto reflections on shiny parts
- ≈ estimates are only valid for square-on photos
- Photos live only on the device; nothing syncs
- README is behind (no crop, dimension or tab-bar docs)
- The claude.ai preview copy is updated by hand and can drift from `index.html`

## Next steps
1. Test on a phone on the shop floor; fix touch issues found.
2. Launch from Slack: channel bookmark now, then `/drcam DR-#### part` slash command that opens a pre-filled link.
3. Split `index.html` into modules (capture / markup / collage) so the markup engine can be reused in the instructions app.
