# Subterra

Bass you feel before you hear it. Subterra is a single-page web app that boosts the low end of any audio track using the Web Audio API — entirely in your browser, with no backend and no uploads.

## What it does

1. **Upload** — drag and drop an MP3 (WAV and OGG also work) or click to browse. Files up to 50 MB.
2. **Pick a level** — one continuous fader rail with three stops:
   - **Warm** — a gentle low-shelf lift at 100 Hz (+8 dB). The low end settles in.
   - **Heavy** — a 90 Hz low shelf (+16 dB) plus a resonant 60 Hz peak (+8 dB, Q 1.0). The subwoofer wakes up.
   - **Destroyed** — a 120 Hz low shelf (+30 dB), peaks at 50 Hz (+20 dB) and 80 Hz (+15 dB), a parallel 120 Hz lowpass for pure sub rumble, tanh soft-clip saturation, a -30 dB high shelf above 1.5 kHz (vocals sink below the rumble), and a limiter at the end so it stays loud rather than broken.
3. **A/B compare** — toggle between the boosted mix and the original while the track plays.
4. **Watch it** — a canvas subwoofer cone pulses with sub-bass energy, and a spectrum analyser emphasises the 20–120 Hz band. At Destroyed the whole room shifts to ember red and shakes.
5. **Download** — render the selected level offline with `OfflineAudioContext`, then export WAV (always available) or MP3 (320 kbps, when the lamejs encoder loads from the CDN).

Everything is tuned from a single `CONFIG` object at the top of the script — filter types, frequencies, gains, limiter settings and file limits all live there.

## Running it

No build step. Open `index.html` directly, or serve the folder:

```bash
npx serve .
# or: python3 -m http.server 8000
```

Then visit the printed URL. First click or keypress resumes the AudioContext (browser autoplay policy).

## Design

"Cinema sound system": late-night dark theatre, subwoofer cone, tungsten projector warmth.

- Palette: sub-black `#06070A`, cone graphite `#15171D`, bone `#ECE7DF`, fog `#8A909D`, tungsten `#F0B35A`, ember `#FF3A1D` (reserved for level 3).
- Type: Big Shoulders Display for oversized condensed headings, Hanken Grotesk for body and UI.
- A 2.39:1 letterbox frame slides open once on load; a film-grain overlay and a soft vignette sit over everything.
- Motion only responds to audio or user actions, and all shake/pulse effects respect `prefers-reduced-motion`.

## Notes

- The MP3 encoder loads from `cdn.jsdelivr.net` (lamejs 1.2.1). If it fails, MP3 export is disabled and WAV export still works.
- Processing is 100% client-side; your audio never leaves the page.
- Level 3 is genuinely loud. Lower your volume first.
