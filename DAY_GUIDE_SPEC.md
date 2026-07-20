# Day Guide — Build Spec
## Productivity Intelligence Innova-thon 2026 · 21 July 2026

Hand this file to Claude Code alongside `PROJECT.md`. Build target: `guide/index.html` in the existing repo, deployed to `https://[user].github.io/[repo]/guide/`.

---

## 1. What this is

A **mobile-only, offline-capable attendee companion** for the day of the event. Not a marketing page — the landing page already does that job. This is a utility: an attendee standing in the MATRADE lobby at 8:05am with one bar of signal needs to know where to go, right now.

Design for the phone in one hand, at arm's length, in a bright hall.

**Primary user:** an attendee who has never been to MATRADE, arriving by car, presenting in a breakout room they can't find.

---

## 2. Architecture

Single self-contained file, same as `index.html`, with three additions:

| File | Purpose |
|------|---------|
| `guide/index.html` | Entire app — CSS + JS inline |
| `guide/sw.js` | Service worker, cache-first, ~30 lines |
| `guide/manifest.json` | Enables "Add to Home Screen" with icon + standalone display |

**Offline is the hard requirement.** MPC hall wifi is a known risk (see risk register in the kertas kerja). Rules:

- No CDN dependencies at runtime. Bebas Neue + DM Sans must be **self-hosted as woff2 in `guide/fonts/`**, not loaded from Google Fonts.
- Photos: compress hard (max 1200px wide, ~80KB each as webp). Do **not** base64-embed here — the service worker caches them fine as separate files and the HTML stays editable.
- Total payload target: **under 800KB**. The landing page's 4.5MB is unacceptable for someone on 4G in a basement car park.
- Service worker: cache-first on install, so second load is instant and airplane-mode-safe. Bump a `CACHE_VERSION` const on every deploy so updates actually land.

**No framework, no build step.** Consistent with the existing project.

---

## 3. Design system

Inherit everything from `PROJECT.md` — same fonts, same palette. This must feel like the same event.

Two deliberate departures, because this is a utility not a showcase:

1. **Dark by default, always.** Teal Deep `#061C24` background throughout. Easier on battery, easier to read in a dim hall, and it makes the gold `#F0C832` "you are here" markers pop.
2. **Larger base type.** Body copy at 16px minimum, tap targets 48px minimum. No `clamp()` display sizes above 48px — there is no desktop version to scale up to.

Motion: restrained. Section transitions, the live progress bar, and the room-finder result reveal. Nothing scroll-triggered — scroll-jacking on touch feels broken.

Respect `prefers-reduced-motion` throughout.

---

## 4. Navigation

**Fixed bottom tab bar**, five tabs, thumb-reachable. Not a hamburger — attendees will switch between these constantly.

```
┌─────────────────────────────────────┐
│                                     │
│           active panel              │
│                                     │
├─────────────────────────────────────┤
│  NOW    GO    MAP   PLAN   HELP     │
└─────────────────────────────────────┘
```

Panels swap via CSS `display` + a 180ms fade; no routing, no page loads. Add `?tab=go` deep-link support so the WhatsApp broadcast can link straight to parking directions.

Keep the EN/BM toggle from the landing page — same `data-en` / `data-bm` pattern, same `localStorage` key so language choice carries over.

---

## 5. Panels

### 5.1 NOW — the signature element

This is the thing that makes the guide worth opening. Everything else is reference material; this is live.

Reads the device clock and renders the current state of the day:

- **Before 08:00** — countdown to doors opening, plus a "what to bring" strip.
- **During the day** — a large card: current session title, speaker, room, and a **progress bar showing how far through the session we are**. Below it, a smaller "Next up at 10:30" strip.
- **After 17:00** — thank-you card, link to the showcase site and the feedback form.

Implementation: a `SCHEDULE` array of `{start, end, title, titleBm, speaker, room, type}` objects with ISO datetimes on 2026-07-21. A `setInterval` at 30s finds the active entry and re-renders. Handle the gaps between sessions ("Break — next session at 14:00") rather than showing nothing.

**Ship a `?t=` debug param** that overrides the clock, so this can be tested on 20 July without changing the system time.

Colour-code by session type using the accents already in the design reference: gold `#B8860B` morning/awards, green `#0E7A56` breakout, pink `#C2185B` lunch, blue `#1565C0` VIP.

### 5.2 GO — getting there

Ordered by what someone needs first.

1. **Address block** — Dewan Produktiviti, MPC, MATRADE, Jalan Sultan Haji Ahmad Shah, Kuala Lumpur. Big, selectable, with a copy button.
2. **Three buttons, full width, 56px tall:** Open in Waze · Open in Google Maps · Call secretariat. Use `waze://`/`https://waze.com/ul?q=` and `https://maps.google.com/?q=` with the address string, plus `tel:` — all work offline because they hand off to another app.
3. **Parking** — [NEEDS INPUT, see §7]. Entrance, levels, rate, and what to do when full. Include a photo of the entrance if you have one; a photo beats a paragraph.
4. **Public transport** — nearest MRT/LRT station and the walk time.
5. **Drop-off point** — where a Grab should stop, which is often not where the car park is.

### 5.3 MAP — venue layout

Not an embedded Google Map — useless indoors. A **hand-drawn schematic as inline SVG**, one per floor, showing:

- Registration counter
- Dewan Produktiviti (main hall)
- Breakout Rooms A / B / C
- Exhibition / vendor booths
- Surau, toilets, refreshments

Tapping a room highlights it and shows a one-line caption. Inline SVG so it scales, works offline, and can be styled with the same palette.

Above the map, the **room finder** — the single most-asked question of the day:

> **Which room am I in?**
> [ Patient Journey ] [ Clinician Journey ] [ Management Productivity ]

Three big buttons. Tap one → reveals "Room A — Level 2, turn right past registration" with the room highlighted on the schematic. This is worth animating: a 300ms reveal with the room pulsing once.

### 5.4 PLAN — full programme

The 08:00–17:00 schedule from the kertas kerja, as an accordion. Reuse `toggleProg()` from the landing page.

Two things the landing page version doesn't need:

- **Auto-scroll to and auto-expand the current session** on panel open.
- A **"● LIVE"** dot on whatever is running now.

Include the three plenary titles and the breakout format (8 min presentation + 4 min Q&A) — presenters will check their slot length repeatedly.

### 5.5 HELP — everything else

Flat list of collapsible items, no cleverness:

- **Wifi** — SSID and password, in monospace, with a copy button. [NEEDS INPUT]
- **Secretariat contacts** — 2–3 names with `tel:` links. [NEEDS INPUT]
- **Emergency** — first aid location, fire assembly point, security. [NEEDS INPUT]
- **Prayer times & surau location** for 21 July, KL.
- **Food** — lunch time, where, and note the calorie tagging (it's in the committee list, so use it).
- **Certificates** — how and when attendees collect them.
- **Feedback form** — link out.
- **Presenter checklist** — arrival time, where to load slides, timing rules, who to find.

---

## 6. Build order

Ship in this sequence so there's always a working version:

1. Shell — tabs, panels, palette, fonts, manifest
2. PLAN (static content, highest value per hour)
3. GO (addresses + map deep links)
4. NOW (live logic)
5. MAP (SVG schematic + room finder)
6. HELP
7. Service worker + offline test in airplane mode
8. Real-device test: iOS Safari and Android Chrome, both in bright light

**Test on an actual phone before the run-through, not just DevTools mobile view.** iOS Safari's toolbar behaviour and `100vh` will bite otherwise — use `100svh`.

---

## 7. Content still needed from you

The build can start with placeholders, but these must be real before 21 July:

- [ ] Car park entrance, levels, rate, overflow plan
- [ ] Which floor and room numbers map to Breakout A / B / C
- [ ] Registration counter location
- [ ] Wifi SSID and password
- [ ] Secretariat phone numbers (2–3 people, on-site)
- [ ] Surau, first aid, and fire assembly locations
- [ ] Grab/taxi drop-off point
- [ ] Nearest MRT/LRT station and walk time
- [ ] Feedback form URL
- [ ] Confirmed final programme times (the tentative schedule has plenary times that may have shifted)

Mark every placeholder in the HTML with `<!-- TODO: -->` so nothing ships as lorem ipsum.

---

## 8. Distribution

- Deploy to `/guide/` in the existing repo
- Generate a QR code pointing at it — put it on the registration desk, the event pass, and the LED backdrop
- WhatsApp broadcast the night before: short link + one line telling people to "Add to Home Screen" so it works without signal
- Put the same link in the nav of the main landing page
