# Discrepancy Cam

A single-file web app (`discrepancy-cam.html`) for taking discrepancy photos, marking them up, and building side-by-side collages.

## What it does
- **Capture**: take a photo with the phone's native camera, use the live camera (lets you take a burst, self-hosted only), import files, or drag/drop or paste an image.
- **Report header**: DR #, part/serial, station, and inspector. These are stamped on every export.
- **Markup**: freehand, arrow, box, circle, text, and **numbered callouts**. Each callout has its own note. You can also select/move, recolor, undo/redo, and use keyboard shortcuts (V P A B C T N, Ctrl+Z / Ctrl+Y, Del).
- **Export**: a PNG with an optional footer showing the report line, the finding, and the callout notes. From there you can Save, Share (phone share sheet → Slack), Copy image (paste into Slack), or Copy notes (text for the thread).
- **Collage**: six layouts, with label presets (Expected/Actual, Acceptable/Reject, Before/After, A/B/C). You can set each panel's photo, label, and color. Other options: 4:3, square, or 3:4 panels, fill or fit, a white or dark background, and a title bar with the DR # and part.
- **Drafts**: photos and markup are saved in the browser (IndexedDB), so a reload doesn't lose work. Nothing leaves the device until you export.

## Hosting (needed for live camera + Slack share)
The camera API and Web Share only work over **HTTPS**. Any static host works. Rename the file to `index.html` and put it on one of:
- an internal web server or intranet
- GitHub Pages / Azure Static Web Apps / S3 + CloudFront (private or SSO-protected)

## Launching from Slack
Pick one, from least to most setup:

1. **Pinned link or channel bookmark**: add the hosted URL as a bookmark in `#quality` (or whichever channel). One tap opens it on a phone.
2. **Workflow Builder shortcut**: create a workflow ("Start DR photos") whose step posts a message with the link. It appears in the channel's shortcut menu.
3. **Slash command** (a custom Slack app): `/drcam DR-2291 4410-032` replies with a button linking to
   `https://<host>/?dr=DR-2291&part=4410-032`. The app reads `dr`, `part`, `station`, and `inspector` from the URL and pre-fills the report. You need a small endpoint (a serverless function) to answer the slash command.

Sending images back to Slack today is done by the user, with the Share or Copy buttons. Fully automatic upload into a DR thread would need a backend holding a Slack bot token, which comes after option 3.

## Toward the instructions app
The markup engine (`drawShape`, `bbox`, `hitShape`, `moveShape`) is plain JS with no dependencies. Markup is stored as vector JSON, not burned into pixels, so the same editor can annotate step images for work instructions. Suggested next step, once the workflow is validated: move this into a repo (Vite + TypeScript) with `markup/`, `capture/`, `collage/` modules shared by both apps.
