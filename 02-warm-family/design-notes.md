# 02 — Porchlight (топло-семейна)

**Pitch:** Практиката, в която водиш цялото семейство — топла като лампа на верандата, сериозна като лекар с 10+ години опит.

## Mood
Sunlit, human, reassuring. Крем-хартия вместо клинично бяло, теракота (clay) вместо „медицинско" синьо/тюркоаз, маслено-жълти акценти като следобедна светлина. Никакво teal, никакъв glassmorphism (съзнателно скъсване с текущия сайт). Grown-up warm — не детски clip-art: сериозна серифна типография + меки органични форми.

## Target patient
Родители, записващи цялото семейство, и тревожни пациенти. Доказателствата, изведени на преден план: чип „Прием на деца", hero-цитатът „Нямах усещане, че съм на зъболекар." (Стефка Р.) и „отношението – човешко и топло" (Лиляна А.) в отзивите.

## Key design moves
1. **Вълнисти SVG разделители** — една и съща вълна (1440×64, `fill: currentColor`) между всички основни секции; тонирана крем/бяло/масло/clay чрез модификатори (`.wave--cream-card` …), обърната с `scaleX(-1)` за разнообразие.
2. **Ръчно-рисуван squiggle** под акцентираната дума „спокойствие" в H1 — маслен щрих (stroke 5, round caps) под clay-курсив Vollkorn.
3. **Пастелни икони-кръгове** към услугите — butter/sage/clay-soft кръгове + stroke-икони (един stroke 1.8 навсякъде: зъб, лупа, искра, коронка, капка, зъб-със-стрелка).
4. **Speech-bubble отзиви** — бели балони с ъгълче (`::after` ромб) и голям декоративен „ знак в масло; автор с кръгъл инициал-аватар. Леки статични наклони (±1°) за човешки ритъм.
5. **Pill-чипове в хирото** — „Прием на деца · НЗОК · BG / EN · 5.0 ★ (356)" + rating-пил върху снимката.
6. **CSS blobs** — органични border-radius петна (butter/sage, ниска опасити) зад хирото и CTA-лентата; `pointer-events: none`, в `overflow: hidden` контейнери.
7. **Затваряща CTA-лента в плътен clay** със „залезни" блобове — бутоните се обръщат (butter-пил + бял ghost), за да остане контрастът AA.

## Token summary

### Palette (hex → роля)
| Token | Hex | Роля |
|---|---|---|
| `--color-cream` | `#FFF7EE` | фон на страницата |
| `--color-card` | `#FFFFFF` | карти, полета, текст върху тъмно |
| `--color-ink` | `#33241A` | заглавия; фон на футъра (14:1 на cream) |
| `--color-text` | `#5C4A3D` | основен текст — **7.9:1** на cream ✓ AA |
| `--color-text-soft` | `#7A6557` | вторичен текст — 5.2:1 ✓ |
| `--color-clay` | `#B04A24` | primary CTA/линкове; бял текст върху него **5.4:1** ✓ |
| `--color-clay-deep` | `#933B1B` | hover |
| `--color-sage` | `#5F7D58` | зелен акцент — САМО декор/едър текст (4.3:1 на cream — под AA за дребен текст) |
| `--color-sage-deep` | `#47603F` | **AA-корекция**: sage за текст/икони — 6.6:1 ✓ |
| `--color-butter` | `#F6C877` | декор, badges — ink върху него 9.5:1 ✓ |
| `--color-butter-soft` / `--color-butter-band` | `#FBE7C2` / `#FDF0DC` | икони-кръгове, consult-карта / топла секция-лента |
| `--color-sage-soft` / `--color-clay-soft` | `#E9EFE5` / `#F8E3D6` | пастелни кръгове, hover-тонове |
| `--line` | `#EFD9C4` | борд/hairlines |

AA бележки: sage от спецификацията остана като декор; за текст добавих по-тъмен `--sage-deep`. Всичко останало мина проверка без промяна на зададените стойности.

### Type
- `--font-display: 'Vollkorn'` (топъл сериф, отличен кирилски) — H1 `clamp(2.1rem, 5vw, 3.2rem)` w600; акцентната дума italic w500 в clay; H2 `clamp(1.55…2.15rem)`; H3 `clamp(1.15…1.3rem)`; числа в статистиките w700.
- `--font-body: 'Nunito'` (заоблен, приятелски) — body `clamp(1rem…1.075rem)` / line-height 1.7; бутони w800; eyebrow w800 uppercase + letterspacing.

### Spacing, radius, shadow logic
- Space: 4px скала (`--space-1…9`: 4→96); секции `clamp(52px, 8vw, 92px)`; контейнер `--wrap: 1080px`.
- Radius: карти 18px (`--radius-card`), снимки/големи панели 28px (`--radius-photo`), полета 12px, всичко останало pill 999px.
- Shadow: една топла сянка с clay-оттенък — `0 10px 30px rgba(147,59,27,.10)` (`--shadow-soft`) + lift/header варианти. Без студени сиви сенки.

## Component inventory
`skip-link` · `site-header` (sticky, бранд-монограм „К", hamburger с aria-expanded/aria-controls/Escape) · `site-nav` · `header-tel` · `btn` (primary / secondary / butter / ghost / sm) · `chips`+`chip` · `badge` („Под микроскоп") · `icon-circle` (butter/sage/clay) · `hero` (+blobs, squiggle, rating-пил, mini-bubble) · `wave` (6 цветови прехода + flip) · `stats`/`stat` · `mini-services`/`mini-card` · `service-cards`/`service-card` · `steps`/`step` (кръгове 01–03 + пунктирана връзка) · `bubbles`/`bubble` (+`bubble--mini`, аватари) · `consult` (банер „Цените се определят след преглед") · `faq` (нативни `details/summary` със стилизиран chevron) · `checklist-card` · `portrait-slot` (кръгъл placeholder с монограм) · `gallery` · `info-card`/`info-row` · `map-slot` (placeholder с pin) · `form-card` + `form-grid`/`form-field`/`select-wrap`/`check-field`/`form-note`/`form-success` · `cta-band` (+`--simple` за контакти) · `site-footer` · `mobile-bar` (fixed ≤720px) · `blob` · reduced-motion неутрализация.

## Porting notes
Всички стойности живеят в `:root` на `styles.css` — палитра/типография/радиуси се пренасят 1:1 като token-речник към build.py шаблона; компонентите са BEM-ish и не съдържат сурови hex-ове, така че смяна на посоката = смяна само на token-блока (+ Google Fonts линка и wave/squiggle SVG-тата като partials).
