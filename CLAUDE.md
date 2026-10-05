# Tijil & Arpita — wedding invitation website

Wedding: Wednesday 2 December 2026 (Tijil Shandilya & Arpita Sharma).

## What this is
A single-page, reel-style invitation (`index.html`) with media in `media/`. No build step, no framework: open `index.html` in a browser or serve the folder (`python3 -m http.server`).

## Page flow
1. Sealed invitation card (maroon doors, gold line-art Ganesh emblem as inline SVG, gold "TA" seal), sized to fill most of the screen (card text scales with `cqw` units). Tap → doors open, petals burst, song fades in, boat video starts. "Open without music" link too. Card only shows when JS runs (`html.js`).
2. Boat scene (`media/boat.mp4`, plays once, holds last frame) — names, TA monogram, date.
3. Shiv–Parvati (`shiv-parvati.mp4`, loops) — blessing line + "request the honour…".
4. Radha–Krishna (`radha-krishna.mp4`, plays once, holds on hands meeting) — "Our Story".
5. Countdown panel (to 2026-12-02 00:00 IST).
6. Haldi (`haldi.mp4`, loops) — event details.
7. Festivities panel: Mehendi, Sangeet, Wedding (highlighted), Reception cards.
8. Venue, RSVP (display-only thank-you; responses are NOT saved), closing panel with families.

## Behaviour notes
- Layout: a 9:16 column (`--col`) centred; on wide screens a blurred copy of the current scene fills the sides (`.ambient`).
- Section blending: each section fades to `--kajal` at its edges, and a scroll-linked `.veil` (opacity only) cross-dissolves between sections. Don't transform the videos on scroll or put `backdrop-filter` over them — both caused lag on phones.
- Videos play only while in view; "once" clips hold their last frame, loops resume where they paused. Never reset `src`/`currentTime` or call `load()` on a clip that's playing — that's what made the opening restart. Clips are buffered in order, one at a time (`warm()`), so each is ready before it's reached. The `.ambient` blur is hidden on portrait screens.
- Music: `media/tum-prem-ho.mp3` ("Tum Prem Ho (Reprise)", supplied by the user), loops, floating disc button to pause/play.
- Fonts: Cinzel (caps), Cormorant Garamond (body), Tiro Devanagari Hindi, from Google Fonts with fallbacks.
- Placeholders are marked `<span class="ph">[…]</span>` — search for `class="ph"` to find everything still to fill in.

## Media
All four clips are Gemini-generated, 720×1280, 10 s (the two loops, `shiv-parvati` and `haldi`, are 9 s: their last second is crossfaded into their start so the loop has no visible jump), re-encoded to H.264 without audio (`-crf 24 -movflags +faststart`). `*.jpg` are first frames (posters), `*-end.jpg` last frames.

## Still to do
- Fill in placeholders: city, story text, event dates/times/venues/dress codes, venue address + map link (`map-link` in script), RSVP date, both families' names.
- Optional clips for Mehendi, Sangeet, Wedding, Reception to give each its own full-screen scene (same pattern as the Haldi section).
- Make RSVP store responses (currently only shows a thank-you).
- Hosted on GitHub Pages from branch `claude/website-github-repo-8pfcqb`, root: https://tijilicious.github.io/Wedding-Invitation/
- A single-file version (all media base64-embedded) can be rebuilt by inlining every `media/...` reference as a data: URI and adding `<!doctype html>` + a viewport meta.
