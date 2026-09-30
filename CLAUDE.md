# Tijil & Arpita — wedding invitation website

Wedding: Wednesday 2 December 2026 (Tijil Shandilya & Arpita Sharma).

## What this is
A single-page, reel-style invitation (`index.html`) with media in `media/`. No build step, no framework: open `index.html` in a browser or serve the folder (`python3 -m http.server`).

## Page flow
1. Sealed invitation card (maroon doors, gold "TA" seal). Tap → doors open, petals burst, song fades in, boat video starts. "Open without music" link too. Card only shows when JS runs (`html.js`).
2. Boat scene (`media/boat.mp4`, plays once, holds last frame) — names, TA monogram, date.
3. Shiv–Parvati (`shiv-parvati.mp4`, loops) — blessing line + "request the honour…".
4. Radha–Krishna (`radha-krishna.mp4`, plays once, holds on hands meeting) — "Our Story".
5. Countdown panel (to 2026-12-02 00:00 IST).
6. Haldi (`haldi.mp4`, loops) — event details.
7. Festivities panel: Mehendi, Sangeet, Wedding (highlighted), Reception cards.
8. Venue, RSVP (display-only thank-you; responses are NOT saved), closing panel with families.

## Behaviour notes
- Layout: a 9:16 column (`--col`) centred; on wide screens a blurred copy of the current scene fills the sides (`.ambient`).
- Section blending: each section fades to `--kajal` at its edges, and a scroll-linked `.veil` + slight video zoom cross-dissolves between sections.
- Videos play only while in view. Media is fetched whole and swapped to blob URLs (`whole()`), because some hosts don't support range requests and iPhone Safari then shows only the poster frame.
- Music: `media/tum-prem-ho.mp3` ("Tum Prem Ho (Reprise)", supplied by the user), loops, floating disc button to pause/play.
- Fonts: Cinzel (caps), Cormorant Garamond (body), Tiro Devanagari Hindi, from Google Fonts with fallbacks.
- Placeholders are marked `<span class="ph">[…]</span>` — search for `class="ph"` to find everything still to fill in.

## Media
All four clips are Gemini-generated, 720×1280, 10 s, re-encoded to H.264 without audio (`-crf 24 -movflags +faststart`). `*.jpg` are first frames (posters), `*-end.jpg` last frames.

## Still to do
- Fill in placeholders: city, story text, event dates/times/venues/dress codes, venue address + map link (`map-link` in script), RSVP date, both families' names.
- Optional clips for Mehendi, Sangeet, Wedding, Reception to give each its own full-screen scene (same pattern as the Haldi section).
- Make RSVP store responses (currently only shows a thank-you).
- Host on GitHub Pages: push this folder to a public repo, Settings → Pages → deploy from main / root. Site will be at https://<user>.github.io/<repo>/.
- A single-file version (all media base64-embedded) can be rebuilt by inlining every `media/...` reference as a data: URI and adding `<!doctype html>` + a viewport meta.
