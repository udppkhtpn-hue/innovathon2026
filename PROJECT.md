# Productivity Intelligence Innova-thon 2026
## Project Context for Claude Code

---

## What this project is

A conference landing page for **Productivity Intelligence Innova-thon 2026**, a national AI healthcare convention organised jointly by **Hospital Tengku Permaisuri Norashikin (HTPN) Kajang** and **Perbadanan Produktiviti Malaysia (MPC)**.

- **Event date:** 21 July 2026
- **Venue:** Dewan Produktiviti, MPC, MATRADE, Kuala Lumpur
- **Theme:** Meningkatkan Produktiviti Melalui Automasi & Transformasi Digital
- **Secretariat email:** hio.htpn@moh.gov.my
- **Live showcase site:** https://htpn-showcase-v2.vercel.app/
- **Document code:** VOL.2026/001

---

## File structure

```
index.html          ← entire homepage, single self-contained file
PROJECT.md          ← this file
images/             ← (future) extract base64 images here to reduce file size
```

All photos and logos are currently embedded as base64 data URIs directly inside `index.html`. When refactoring, move them to an `images/` folder and reference them with `<img src="images/filename.jpg">`.

---

## Design system

### Inspired by
RenderATL.com — editorial, asymmetric, high-energy conference aesthetic.

### Fonts (Google Fonts)
| Font | Usage |
|------|-------|
| `Bebas Neue` | All headings, section titles, nav, CTAs, stats, buttons |
| `DM Sans` | Body copy, captions, form labels (weight 300/400/500) |

### Colour palette
| Name | Hex | Usage |
|------|-----|-------|
| Teal Deep | `#061C24` | Page background, darkest sections |
| Teal Dark | `#0A2C35` | Hero bg, dark sections, nav |
| Teal Accent | `#1D9E75` | Green accent, bullets, checkmarks |
| Teal Light | `#5DCAA5` | Secondary green, eyebrow labels |
| Yellow | `#F0C832` | Primary accent — CTAs, asterisk, borders, marquee bg |
| Pink | `#F472B6` | Secondary CTA buttons, eyebrow pills, comparison divider |
| Cream | `#F4F0E6` | Light section backgrounds |
| Paper | `#F3EFE3` / `#E8E4DA` | Partners/experience section bg with noise texture |
| Ink | `#1A120A` | Dark text on cream sections |
| White | `#FFFFFF` | Text on dark sections, logo card backgrounds |

### Key design patterns
- **Torn paper edges** between dark/cream sections via CSS `clip-path: polygon()`
- **Rotated polaroid cards** in stats section — each card rotated ±4° with colour bottom half
- **Yellow marquee ticker** — `transform: rotate(-1deg)`, `background: #F0C832`, Bebas Neue text
- **Asymmetric hero photo frame** — rotated 2°, gold `#F0C832` border, hover straightens
- **Speaker photo frames** — overlapping, rotated, gold border, greyscale → colour on hover
- **Spinning asterisk** — 8-point SVG star in yellow, `animation: spin 10s linear infinite`
- **Offset box shadows** — buttons use `box-shadow: 4px 4px 0 #000` (no blur)
- **Logo ticker rows** — two rows scrolling in opposite directions, white cards, fade edges
- **Programme accordion** — click to expand, colour-coded left borders per session type

---

## Page sections (in order)

| # | Section | ID/Class | Background |
|---|---------|----------|------------|
| 1 | Sticky Nav | `#mainNav` | Transparent → `#061C24` on scroll |
| 2 | Hero | `.hero` | `#0A2C35` + MATRADE photo bg |
| 3 | Marquee strip | `.marquee-wrap` | `#F0C832` yellow, rotated |
| 4 | Stats polaroids | `.stats-section` | `#061C24` |
| 5 | Strategic Collaboration (logo tickers) | `#partners` | `#E8E4DA` concrete texture |
| 6 | Why HTPN × MPC | `.why-section` | `#0A2C35` |
| 7 | Featured Speakers | `#speakers` | `#0A0A0A` |
| 8 | The Experience | `#showcase` (experience) | `#F3EFE3` cream + torn edges |
| 9 | One Badge | `#register` | `#0A0A0A` |
| 10 | Why Clinicians Choose Innova-thon | `.comparison-section` | `#0A0A0A` |
| 11 | Full Day Programme (accordion) | `#programme` | `#F3EFE3` cream |
| 12 | Before You Arrive (3 cards) | `.practical-section` | `#F3EFE3` cream |
| 13 | See The Work (showcase link) | `.gallery-section` | `#061C24` |
| 14 | Closing CTA | `#register-form` | `#0A2C35` + MATRADE photo |
| 15 | Footer | `footer` | `#030c10` |

---

## Key people

| Name | Role | Section |
|------|------|---------|
| Dr Hj Muhd Siv Azhar Merican | Pengarah HTPN, Advisor | Footer, Programme |
| Dr Ferwahn Fairis bin Ab Karim | Penyelaras HIO, Main Coordinator | — |
| Dr Naim bin Abdul Malek | HIO Technical Team | — |
| Dr Muhammad Syafiz bin Ruzain | HIO Technical Team | — |
| Prof Madya Dr Mohd Rafee bin Baharudin | Keynote Speaker — Plenary 1 (9am) | Speakers |
| Prof Madya Dr Shukor Sanim bin Mohd Fauzi | Keynote Speaker — Plenary 2 (9:30am) | Speakers |
| Dr Ahmad Hakiim Jamaluddin | Keynote Speaker — Plenary 3 (10am) | Speakers |

---

## Featured speakers — plenary titles

**Prof Madya Dr Mohd Rafee (UPM — Faculty of Medicine & Health Sciences)**
> *"Navigating the AI Revolution: Transforming Malaysia's Healthcare System Through Intelligent Technologies"*

**Prof Madya Dr Shukor Sanim (UiTM Perlis — Faculty of Computer & Mathematical Sciences)**
> *"Funding the Future: How to Secure Research Grants, Build University–Hospital Partnerships, and Scale AI in Clinical Environments"*

**Dr Ahmad Hakiim Jamaluddin (UPM — Dept of Mathematics & Statistics)**
> *"Engineering a Culture of Innovation: How Reward Systems, AI Competitions and Recognition Frameworks Unlock Institutional Creativity"*

---

## Competition — Innova-thon

- **Target:** 50 model applications
- **3 breakout rooms:**
  - Room A: Patient Journey / Customer Experience
  - Room B: Clinician Journey / Predictive Modelling
  - Room C: Management Productivity / Dashboard
- **Format:** 8-min presentation + 4-min Q&A per project
- **Prizes:** Gold RM500 | Silver RM300 | Bronze RM200 | 5× Consolation RM100
- **5 phases:** Registration (May) → Pre-assessment (June) → Mentorship (Jun–Jul) → Finals (21 Jul) → Awards (4:30pm)
- **Judging rubric:** Problem Statement · Creativity · User Friendly · Deployment · Data Validation · Output/Outcome · Scalability · Sustainability

---

## Strategic partners & logos

All logos embedded as base64 in the logo ticker section. Files in `images/` folder when refactored:

| Key | Organisation | Type | File |
|-----|-------------|------|------|
| htpn | HTPN Kajang | Co-Organiser | logo_HTPN_Kajang.jpeg |
| mpc | MPC Malaysia | Co-Organiser | (text card — no logo file) |
| kkm | Kementerian Kesihatan Malaysia | Strategic Partner | logo_kkm.jpeg |
| upm | Universiti Putra Malaysia | Academic | UPM_logo.jpg |
| uitm | Universiti Teknologi MARA | Academic | Logo_UITM.jpg |
| utm | Universiti Teknologi Malaysia | Academic | LOGO-UTM.png |
| mimos | MIMOS Berhad | R&D | logo_MIMOS.png |
| ikn | Institut Kanser Negara | Health | logo_IKN.jpeg |
| rocketz | Rocketz Sdn Bhd | Platform AI | (text card — no logo file) |
| microsoft | Microsoft | Industry | logo_microsoft.jpg |
| hpp | Hospital Pulau Pinang | Hospital | Logo_HPP.png |
| hsa | Hospital Sultanah Aminah JB | Hospital | logo_HSA.png |
| hkb | Hospital Kepala Batas | Hospital | logo_HKB.jpeg |
| jkn | JKN Sarawak | Dept of Health | logo_JKN_Sarawak.jpeg |
| unimap | UniMAP | Academic | logo_UniMAP.svg |

---

## Real photos embedded (base64)

| Photo | Used in | Object position |
|-------|---------|----------------|
| MATRADE building exterior | Hero background, Closing CTA, Practical card | `center 30%` |
| Convention hall (laser lights, packed audience) | Hero right frame, Gallery main | `center 40%` |
| MOH Mental Wellbeing App on screen | Stat card 1 (pink), Gallery cell 1 | `center top` |
| HIO training session classroom | Stat card 3 (dark) | `center 30%` |
| HTPN 1889 original building | Stat card 4 (teal), Gallery cell 2 | `center 40%` |
| HIO team mentoring session | Why HTPN section (right col video replacement) | `center 35%` |
| MPC team at #aiPRODUKTIVITI sign | The Experience section (left col) | `center 45%` |
| Prof Madya Dr Mohd Rafee headshot | Speaker frame 1 | `center top` |
| Prof Madya Dr Shukor Sanim headshot | Speaker frame 2 | `center 15%` |
| Dr Ahmad Hakiim headshot | Speaker frame 3 | `center 20%` |
| HTPN HIO Showcase screenshot | Gallery full-width clickable cell | `center top` |

---

## Bilingual system

- Toggle: **EN** (default) / **BM**
- Implementation: `data-en` and `data-bm` attributes on text elements
- JS function: `setLang('en')` / `setLang('bm')`
- Preference stored in `localStorage`

---

## Mobile breakpoints

| Breakpoint | Target |
|-----------|--------|
| `max-width: 768px` | Tablets and phones |
| `max-width: 430px` | Small phones (iPhone SE, mini) |
| `@supports (-webkit-touch-callout: none)` | iOS Safari specific |
| `@media (hover: none) and (pointer: coarse)` | Touch devices — disables hover effects |

### Key mobile rules
- Stats section: `display: grid; grid-template-columns: 1fr 1fr` (remove rotations)
- Speakers: stack vertically, photo frames `position: relative`
- Comparison fan: stack vertically, `transform: none`
- Badge tiles: `grid-template-columns: 1fr 1fr`
- Hamburger menu: full-screen overlay, Bebas Neue links
- Hero: `min-height: 100svh` for iOS toolbar fix
- Fonts: async-loaded via `media="print" onload`

---

## JavaScript functions

| Function | Purpose |
|----------|---------|
| `setLang(lang)` | Bilingual EN/BM toggle |
| `toggleMenu()` | Mobile hamburger menu open/close |
| `toggleProg(header)` | Programme accordion expand/collapse |
| `countUp(el, target, duration, suffix)` | Animated number count-up on scroll |
| IntersectionObserver `.reveal` | Scroll-triggered fade-in animations |
| IntersectionObserver `.stat-num` | Triggers count-up when stats visible |
| Scroll listener `#mainNav` | Nav background darkens after 80px scroll |

---

## Known issues / future improvements

- [ ] File is ~4.5MB due to base64 embedded images — refactor to `images/` folder for faster loading
- [ ] Add MPC logo when available (currently text card)
- [ ] Add Rocketz logo when available (currently text card)
- [ ] Add remaining judge headshot photos (Dr Izhar, Dr Ishak, Dr Nash, etc.)
- [ ] Add Google Form embeds to `/register` page
- [ ] Build remaining 7 sub-pages: compete, speakers, programme, showcase, pre-convention, partners, register
- [ ] Connect Google Sheets for app showcase data
- [ ] Add Facebook Live link when available

---

## GitHub Pages deployment

- Repo: upload as `index.html` to root of public repository
- URL pattern: `https://[username].github.io/[reponame]/`
- Enable: Settings → Pages → Deploy from branch → main → / (root)
- Update cycle: re-upload `index.html` → auto-rebuilds in ~2 minutes

