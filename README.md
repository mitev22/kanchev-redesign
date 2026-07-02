# Kanchev Dental — Redesign Explorations (Phase 1)

**Live:** https://mitev22.github.io/kanchev-redesign/ — Bulgarian gallery · English: https://mitev22.github.io/kanchev-redesign/index.en.html (use the БГ/EN toggle in any header to switch). *Demonstration site; not yet officially affiliated with the practice.*

Six genuinely distinct design directions for the site of **Дентална практика д-р Иван Кънчев (Пловдив)** — each a lean, self-contained 4-page site (Начало · Услуги · За доктора · Контакти) built as zero-build static HTML/CSS/JS, **fully bilingual (BG + EN)** with a language toggle on every page. **Open `index.html` in any browser** (double-click — no server, no build step) to see the comparison gallery, or use the live link above; every card links into a direction. All six reuse the *identical, real* content extracted from the current live site (`clinics/kanchev-dental/index.html`), so you are comparing pure design language, not different copy. The only external dependency per direction is its Google Fonts pairing (pages fall back to system fonts offline).

Each Bulgarian page (`index.html`, `services.html`, …) has an English sibling (`index.en.html`, `services.en.html`, …) with the same design; the English content is a faithful translation of the same real source (reviews translated from the Bulgarian originals).

## The six directions

| Folder | Name | One-line rationale |
|---|---|---|
| `01-modern-clinical` | **Protocol** | Calm white precision — hairlines, numbers, azure accent; the clinic that runs on time. |
| `02-warm-family` | **Porchlight** | Warm cream, rounded serif softness, waves and pills — the whole-family practice. |
| `03-luxury-cosmetic` | **Atelier** | Ivory quiet-luxury editorial with bronze hairlines — monetizes the Siena prosthodontics specialty. |
| `04-bold-playful` | **Milk Tooth (Млечен зъб)** | Poster-loud, sticker-covered, zero-fear — the deliberately unconventional option no cautious agency would pitch. |
| `05-editorial-minimal` | **Broadsheet** | Photo-free, typography-led broadsheet with one vermilion accent — candor instead of brochure. |
| `06-dark-instrument` | **Instrument** | The dark option, but *warm* (espresso + brass, mono labels) — built around the real differentiator: лечение под микроскоп. |

Each direction folder contains `index.html`, `services.html`, `about.html`, `contact.html`, a shared `styles.css` (design tokens in `:root` + reusable components — the portable design system), `design-notes.md` (aesthetic, mood, target patient, key moves, token summary), and `assets/` with the practice's real photos where the direction uses photography.

## What's real vs. placeholder

**Real (verbatim from the live site):** headline, positioning copy, all 6 services + descriptions, all 6 SuperDoc reviews (5.0 · 356), credentials (МУ-Пловдив 2016, Здравен мениджмънт 2023, University of Siena 2024, БЗС), FAQ, 3-step process, „цените се определят след преглед" banner, phone (0896 666 828), hours, НЗОК/деца/EN, GDPR consent text + link to the live privacy policy, and the real operatory/waiting-room photos.

**Placeholder-marked (`<!-- PLACEHOLDER: swap with real content -->` — grep for it):**
- **Address** — бул. Мария Луиза 70, ет. 1 is real but **temporary** (renovation, per `_sales/data-verification.md`); confirm before any direction goes live.
- Doctor portrait slot (no photo of д-р Кънчев exists yet).
- Map embed slot (styled placeholder; live site uses a Google Maps iframe).
- Booking form wiring (demo handler only; Phase 2 reconnects Web3Forms).

No public email exists for the practice, so none is shown (matches the live site). No new factual claims were invented anywhere.

**Comparison hygiene:** the current live design (light teal glassmorphism) and the three older dark drafts in the repo (`cinematic` / `editorial` / `futuristic`) were treated as already-explored territory — none of the six reuses their palettes or languages.

## Phase 2 — porting the winner

**Detected stack:** fully static, zero-framework sites deployed on GitHub Pages — hand-maintained single-file flagship repos (`clinics/kanchev-dental`, `clinics/petkova-dental`) plus the parametrized Python generator **`plovdiv-dental/build.py`** (template + `clinics.json`) that renders the 15-site batch. The winning direction's tokens + components port as the new `build.py` template and get promoted to the flagship repo(s), which is how one winner rolls out across all 17 dental sites.

**To start Phase 2:** reply with the winning folder name, e.g. `port 02-warm-family into the real site` (add "and roll out to the batch" if the 15 spec sites should be restyled too). The port will preserve the live sites' must-keeps: Web3Forms key + botcheck, GDPR consent → `privacy.html`, spec-demo footer, schema.org (Dentist + FAQPage), OG smart-link card + favicon, „цени след преглед" (no price tables), and verbatim reviews.

*Phase 1 changed nothing outside this folder — `clinics/` and `plovdiv-dental/` are untouched.*
