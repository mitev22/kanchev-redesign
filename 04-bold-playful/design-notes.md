# 04 — Milk Tooth / Млечен зъб (смело-игрива)

**One-line pitch:** Зъболекарят, при когото децата (и възрастните със страх) искат да се върнат — постер-енергия, дебела мастилена линия и истински факти, залепени като стикери.

Това е **съзнателно ръбът-на-възможното направление** — вариантът, който предпазлива агенция никога не би предложила. Ако другите пет са „безопасни", това е тестът колко смелост носи брандът. Тезата идва директно от отзив №6: „Нямах усещане, че съм на зъболекар."

## Mood
Loud, joyful, zero-fear. Neo-brutalist-adjacent, но ПРИЯТЕЛСКИ: твърди сенки без blur, 3px мастилен контур върху всичко, ротирани стикери, маркер-подчертавания, маскот-зъбче с усмивка. Под шума — професионализъм: всички твърдения са реални (5.0 · 356, НЗОК, деца, BG/EN, микроскоп), нула измислени обещания.

## Target
Млади семейства, Gen-Z/millennial Пловдив, хора със страх от зъболекар. Съзнателно НЕ таргетира консервативния 60+ пациент (него го хващат направления 01/02).

## Key design moves
1. **Rotated sticker badges** — pill + 3px ink border + hard shadow, ±2.5–5°; само реални факти („5.0 ★ 356 ОЦЕНКИ", „РАБОТИМ С НЗОК", „ПРИЕМ НА ДЕЦА", „СПЕШНИ СЛУЧАИ — ОЩЕ ДНЕС", „BG / EN").
2. **CSS marquee band** (hero → services): дублирани inline списъци + `translateX(-100%)` keyframes, ★ разделители; `aria-hidden` (фактите съществуват като реален текст другаде); статичен под reduced-motion.
3. **Marker highlight** върху една дума в H1 (skewed --sun блок, ink текст) — на всяка страница; във футъра се превръща в „тиксо" (пълен sun блок с ink текст върху ink фон).
4. **Tilted cards** — редуване rotate(±1.2deg); при hover се изправят и сянката расте 5px→8px (само под `prefers-reduced-motion: no-preference`).
5. **Tooth mascot** — геометричен inline-SVG (бяло тяло, розови бузи, sun искра, 5px ink stroke): голям в hero, мини-версия като bullets (tooth-list) и в polaroid-плейсхолдъра за портрета.
6. **Chunky buttons** — 3px border + hard shadow; `:active` се „вдава" в сянката (translate 5px,5px → shadow 0).
7. **Color-blocked sections** — paper → sun marquee → mint-tint → paper → pink-tint → cobalt CTA band; тинтовете дишат, чистите цветове удрят.

## Token summary
| Token | Value | Note |
|---|---|---|
| --color-paper | #FFFDF4 | фон |
| --color-ink | #14131A | текст + всички бордъри/сенки |
| --color-cobalt | #2038E8 | ЕДИНСТВЕНАТА повърхност с бял текст (7.5:1); линкове върху paper (7.4:1) |
| --color-pink | #FF5D8F | само фон, ink текст (6.3:1); НИКОГА като текст върху paper (2.9:1 — fail) |
| --color-sun | #FFC700 | primary бутон/маркер, ink текст (10.9:1) |
| --color-mint | #35C4B5 | фон/акцент, ink текст (8.5:1) |
| --color-card | #FFFFFF | карти |
| + тинтове | #E3F5F1 / #FFE9F0 / #FFF3CE | секционни фонове |
| --font-display | Unbounded 500/700/900 | ШИРОК — H1 clamp(1.7rem,4.5vw,3rem), консервативно за дълги BG думи |
| --font-body | Rubik 400/500/700 | топъл гротеск, кирилица |
| --border | 3px solid ink | върху карти/бутони/инпути/секционни ръбове |
| --shadow-hard(-sm/-lg) | 3/5/8px 0-blur ink | никакъв blur — това Е стилът |
| --radius | 14px (999px pill) | |

**AA бележки:** focus outline е cobalt върху светло, но **sun върху cobalt/ink** (cobalt върху тъмно пада под 3:1). Звездата в рейтинга е ink, не sun (декоративна + съседен текст). Ревю №4 е на английски → `lang="en"`.

## Component inventory
`.skip-link` · `.header` (sticky, no-JS fallback: нав-списък в потока) · `.brand__mono` (ротиран „К") · `.nav` / `.nav-toggle` (JS dropdown, Escape затваря) · `.btn` (--primary/--cobalt/--big) · `.sticker` (--sun/--pink/--mint × --r1..r4) · `.eyebrow` · `.highlight` / `.marker-rule` · `.hero` + `.photo-frame` (+ `__sticker`, `--r`) · `.hero__mascot` · `.stats`/`.stat` · `.marquee` · `.card` + `.tilt-l/.tilt-r` · `.service-grid`/`.service-card` + `.chip` (--pink/--sun/--mint/--cobalt) · `.steps`/`.step__num` · `.review`/`.review-grid` · `.consult` · `.cta-band` · `.footer` · `.mobile-bar` (fixed ≤720px) · `.faq` (details/summary, `--fear` mint вариант с „БЕЗ СТРАХ" стикер) · форми: `.form-grid(--2col)`, `.field`, `.select-wrap` (CSS-триъгълник, без икони-шрифтове), `.check`, `.form-success` · `.call-card` · `.info-card` · `.map-placeholder` (starburst pin) · `.creds` (номериран манифест) · `.polaroid` · `.tooth-list` · `.visually-hidden`.

## Porting notes
- Всички raw hex са само в `:root`; компонентите ползват `var()` — палитрата се сменя от едно място.
- 3px-контурът + hard shadow са отделни токени (`--border`, `--shadow-hard*`) — „омекотяване" на направлението = сваляш на 2px/б blur, без да пипаш компоненти.
- Marquee, tilts и hover-мotion живеят изцяло в `@media (prefers-reduced-motion: no-preference)` — reduced-motion получава статичен, пълноценен сайт.
- Ротираните елементи са в контейнери с padding + `overflow-x: clip` на html/body — нищо не стърчи на 360px.
- Формата е demo (preventDefault → success). Phase 2: Web3Forms (access_key в HTML коментара над формата).
- Адресът е ВРЕМЕНЕН (ремонт, по SuperDoc) — маркиран с PLACEHOLDER/NOTE коментари при всяка употреба; портрет и карта са плейсхолдъри със същите маркери.
- Без имейл никъде — не е измислян.
- Ако направлението спечели: следващи стъпки са OG-мета, реален портрет в polaroid рамката, истинска карта (static image, пак без iframe) и лек entrance-motion (пак зад reduced-motion гейт).
