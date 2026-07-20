# VENUE.md — Innova-thon 2026
Dewan Produktiviti, MPC, MATRADE, Kuala Lumpur · 21 July 2026

Flat facts for the GO and MAP panels of `guide/index.html`. Photos live in `guide/images/`.

---

## Parking
Name: Amphitheatre Parking MATRADE
Rate: RM7 flat
Maps: https://maps.app.goo.gl/yeSXkJa411xBGrG29
TODO: levels / capacity / overflow plan / walk time to lobby

## Arrival route — 5 steps, ground floor to MPC Level 1

1 · MATRADE Entrance
Maps: https://maps.app.goo.gl/TSSF5EYeefSqmo997?g_st=iw
Photo: matrade-entrance.webp

2 · MATRADE Lobby
Landmark: main information counter
Photo: matrade-lobby-info-counter.webp

3 · Escalator to MPC  ← only decision point on the route
Location: behind the main lobby counter, near Richiamo Cafe, across the MPC atrium
Action: take the RIGHT escalator up to MPC, Level 1
Photo: mpc-escalator.webp

4 · MPC Entrance, Level 1
Photo: mpc-entrance-level1.webp

5 · MPC / Innova-thon Registration Counter
Photo: registration-counter.webp
TODO: opening time (programme says 08:00 registration — confirm counter opens earlier)

## MPC Level 1 — event floor layout
Plan: mpc-level1-floorplan.webp (annotated, source of truth for the MAP panel)

The floor runs east–west as two parallel bands with a circulation spine between them.

```
   W                                                             E
   ┌──────────────────────────────────────────────────────────────┐
 N │ TANDAS   DEWAN PRODUKTIVITI   LIFT    BILIK    BILIK         │
   │ TANGGA 8   (Breakout 1 +     BARANG   JURI     SEKRETARIAT   │
   │             plenary hall)                        TANGGA 9    │
   ├───────── MAIN ENTRANCE/EXIT (west, into Dewan) ──────────────┤
   ├─────────────────── circulation / waiting ────────────────────┤
 S │ SURAU     BILIK INOVASI      BILIK TRANSFORMASI    SURAU     │
   │ (lelaki)  (Breakout 2)       (Breakout 3)      (perempuan)   │
   │        ▲ ESKALATOR (TURUN)   ESKALATOR (NAIK) ▲              │
   │          TANGGA 6         MAIN ENTRANCE/EXIT · PENDAFTARAN   │
   └──────────────────────────────────────────────────────────────┘
```

### Breakout room mapping — CONFIRMED
| Breakout | Room | Theme (per programme) |
|---|---|---|
| Breakout Room 1 | DEWAN PRODUKTIVITI | Patient Journey / Customer Experience |
| Breakout Room 2 | BILIK INOVASI | Clinician Journey / Predictive Modelling |
| Breakout Room 3 | BILIK TRANSFORMASI | Management Productivity / Dashboard |

Assumption: Breakout 1/2/3 = programme's Room A/B/C in order. Confirm theme mapping before the room finder ships — the rooms are confirmed, the theme pairing is inferred.

Rooms
- DEWAN PRODUKTIVITI — main hall, north-west. Plenaries, VIP session, awards, AND Breakout Room 1.
- BILIK INOVASI — south, centre. Breakout Room 2.
- BILIK TRANSFORMASI — south, centre-east. Breakout Room 3.
- BILIK JURI — north, centre-east. Jury room, not for delegates.
- BILIK SEKRETARIAT — north-east, next to Tangga 9. Staff/secretariat.
- PENDAFTARAN — south-east, at the top of the up escalator, beside the east Main Entrance/Exit.

Entrances
- Two MAIN ENTRANCE/EXIT points: west (into Dewan Produktiviti area) and south-east (beside Pendaftaran, where the up escalator arrives).

Facilities
- Tandas (toilets) — north-west near Tangga 8; further toilets north-east near Tangga 9.
- Surau (lelaki / male) — west end of south band.
- Surau (perempuan / female) — east end of south band.
- Escalators — NAIK (up, arriving) south-east; TURUN (down, leaving) south-centre. They are NOT the same escalator; leaving delegates walk west.
- Stairs — Tangga 6 (south-centre), Tangga 8 (north-west), Tangga 9 (north-east).
- Lift Barang — goods lift, centre-north. Staff only; useful for equipment load-in.

### Wifi — CONFIRMED
- SSID 1: `Innovathon@Produktiviti`
- SSID 2: `Innovathon@Transformasi`
- Password (both): `P@ssw0rd123`
- Guidance for HELP panel: connect to whichever SSID is stronger where you are; names suggest one access point serves the Dewan end and one the Transformasi end.

TODO on this floor: first aid point, fire assembly point.

## Food
LaUK Kampung Restoran — Ground Floor
Photo: lauk-kampung-restoran.webp
TODO: is this the delegate lunch venue or just an on-site option? opening hours?

## Still missing (nice to have, none block launch)
- Confirm theme ↔ breakout pairing (rooms confirmed; A/B/C order inferred)
- Secretariat on-site phone numbers (2–3)
- First aid point, fire assembly point
- Grab / taxi drop-off point
- Nearest MRT/LRT station + walk time
- Feedback form URL

---

## Notes for the build
- The route is a linear 5-step stepper, one photo per step. Someone is walking this while reading — one step on screen at a time, not a gallery.
- Step 3 carries three landmarks and a left/right choice. It is where people get lost. Give it more visual weight than the others.
- Images: six route photos at 602px wide (37–73 KB each) plus the floor plan at 1600px (99 KB). ~430 KB total — still inside the 800 KB payload budget in DAY_GUIDE_SPEC.md §2.
- MAP panel: do not ship the floor plan image as the map. It is a CAD drawing, unreadable on a phone in a bright hall. Redraw it as inline SVG from the wireframe above — six labelled boxes, the escalator arrows, and the spine. Keep the photo as a tap-to-zoom fallback.
- Source doc numbers both registration and the restaurant as "5"; renumbered above, restaurant split into its own section since it is ground floor and off-route.
- Source doc says "MPC antrum" — read as atrium. Confirm before it ships as signage wording.
