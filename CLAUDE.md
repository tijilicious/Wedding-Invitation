# Tijil & Arpita — wedding invitation website

Live: https://tijilicious.github.io/Wedding-Invitation/ (GitHub Pages, branch `claude/website-github-repo-8pfcqb`, root). Wedding: Wednesday 2 December 2026, Golden Stone Resort, Aligarh. Invitation is from the groom's side.

## What this is
One page (`index.html`) plus `media/`. No build step: open `index.html` or serve the folder (`python3 -m http.server`).

## Flow (story mode)
0. Sealed card: maroon doors, gold Ganesh emblem (inline SVG), "TA" seal; sized with container units (`cqw`). Tap → doors open, petals, song fades in. "Open without music" too. Card only shows when JS runs (`html.js`). Personal greeting from `#Gaur-Family` or `?to=Gaur+Family` ("Dear Gaur Family").
1. Boat (`boat.mp4`) — names, TA monogram, date, Aligarh, countdown to the baraat (2 Dec 2026 18:00 IST).
2. Shiv–Parvati (`shiv-parvati.mp4`) — "Shri Atul Sharma & Smt Renu Sharma … wedding of their son Tijil with Arpita, daughter of Shri R.K. Sharma, Aligarh".
3. Radha–Krishna (`radha-krishna.mp4`) — ॥ सखा सप्तपदा भव ॥ (Saptapadi, seventh vow).
4. Celebrations over `mandap.mp4` — timeline: Haldi (2 Dec, 12 noon, venue not given), Baraat (2 Dec, 6 PM, Golden Stone Resort, directions + Google Calendar), Vadhu Aagman (3 Dec, morning).
5. Closing over `haldi.mp4` — blessings of Late Shri Ramkishore Sharma & Late Smt Malti Devi; hosts Shri Atul Sharma & Smt Renu Sharma and family, Aligarh.

Not included by request: mandap/tilak, mehendi, sangeet, reception, RSVP, phone numbers, विनीत/बाल आकांक्षा section, "our story" text.

## Behaviour
- Autoplays like Instagram stories: `data-dur` seconds per scene (just under each clip's length), progress bars on top, Back / Next (Replay on the last scene) / music at the bottom; tap left third = back, elsewhere = next; hold = pause; arrow keys work. Scrolling by hand pauses autoplay.
- Every clip loops. Entering a scene restarts its clip only if it is paused. Never reset `src`/`currentTime` or call `load()` on a playing clip (caused restarts). Clips buffer in order with `warm()`.
- Cross-dissolve between scenes is a scroll-linked `.veil` (opacity only). Don't transform videos on scroll or put `backdrop-filter` over them — both lag on phones. `.ambient` blur is hidden on portrait screens.
- Hindi/English toggle: elements carry `data-hi`; English is captured from innerHTML at load; choice saved in localStorage.
- Music: `media/tum-prem-ho.mp3` ("Tum Prem Ho (Reprise)", supplied by the user), original file minus its last 12 s with a 2 s fade. Starts at 43.8 s (`SONG_START`) and loops back there. It is fetched whole into a blob so the seek works on any host. Music itself ends ~4:40 (speech after).
- WhatsApp/OG preview: absolute `og:image` = `media/og.jpg` on the Pages URL.

## Media
Gemini-generated, 720×1280, H.264, no audio, `-movflags +faststart`. `shiv-parvati` and `haldi` are 9 s with the last second crossfaded into the start (seamless loop). `mandap.mp4` is the first 12 s of the user's 20 s clip played forward then reversed (24 s seamless loop). `*.jpg` are posters.
