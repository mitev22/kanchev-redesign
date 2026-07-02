# 06 — Instrument (тъмна прецизност)

**One-line pitch:** Топло-тъмен, „инструментален" дизайн — есспресо-кафяво + месинг/кехлибар — който превръща реалния диференциатор на практиката (лечение под микроскоп, половинчасови сегменти, прецизност) в самата визуална идентичност: сайтът изглежда като висок клас оптичен инструмент в кожен куфар.

## Mood

Прецизен оптичен инструмент. Топла тъмнина (espresso/graphite), месингови акценти, mono-етикети като гравирани скали, ретикул (мерна решетка) като брандинг графика. Премиум-спокойно, никога „gamer/neon". Снимките са десатурирани и рамкирани като спесимен-плочи с mono-надписи.

## Target

Пациенти, които избират зъболекар по технология и прецизност (ендодонтия под микроскоп); хора, които резервират вечер/нощем — тъмният интерфейс е комфортен; двуезични пациенти (BG/EN).

## Key design moves

1. **Reticle motif** — фина SVG кръгова мерна решетка (тънки окръжности + tick-марки чрез `stroke-dasharray`/`pathLength`) зад hero-панела, във flagship-услугата, в CTA-лентите и като crosshair в map-плейсхолдъра; малък crosshair-tick маркира всяко section eyebrow.
2. **Mono status chip** — „● ПРИЕМА НОВИ ПАЦИЕНТИ" с пулсираща кехлибарена точка (статична при reduced-motion).
3. **Spec-sheet rows** — `[ ЕТИКЕТ ] стойност` двойки (JetBrains Mono, скобите са CSS pseudo — не се четат от screen readers) за квалификации, прием, контактна информация.
4. **Service panels** — mono индекси „01"–„06", тънки amber stroke-икони в рамкирани квадрати, hover = amber border + мек glow; на services.html панел 01 („Кореново лечение" · таг ПОД МИКРОСКОП) е уголемен flagship с ретикул.
5. **Stat tiles** — панели с големи Golos-числа (10+ / 356 / 5.0 / НЗОК) и mono-надписи.
6. **Specimen plates** — реалните снимки в 1px рамки, `saturate(.85)`, mono-caption + „Панел 01/02" индекс.
7. **Instrument grid** — едва доловима координатна мрежа (~3% топло-бяло) само в hero/page-head и в map-канваса; corner-ticks по CTA-лентите.
8. **Reveal on scroll** — IntersectionObserver + лек stagger; съдържанието е видимо по подразбиране, JS добавя скритото състояние само когато работи И motion е позволен.

## Token summary

| Token | Value | Роля |
|---|---|---|
| `--color-bg` | `#161310` | топло кафяво-черно |
| `--color-panel` / `--color-panel-2` | `#1E1A15` / `#262119` | панели |
| `--color-field` | `#221E19` | form инпути |
| `--color-ink` | `#EFE8DC` | основен текст (≈15.2:1 на bg) |
| `--color-muted` | `#AC9F8D` | вторичен текст (≈7.1:1 на bg, ≈6.2:1 на panel-2 — AA за малък текст навсякъде) |
| `--color-amber` | `#D9A441` | акцент; ≈8.2:1 срещу bg → става и за малък текст; бутоните са amber с тъмен текст (`--color-on-amber #161310`, ≈8.2:1) |
| `--line` / `--line-strong` | `#352D24` / `#4A4032` | 1px рамки |
| `--glow` | `rgba(217,164,65,.12)` | меки сияния (`--shadow-glow*`) |
| Type | Golos Text 500–700 (display), Inter 400/500 (body), JetBrains Mono 400/500 (micro-labels 11px/.12em UPPERCASE) | всички с кирилица |
| Radius | 10px панели, 8px бутони | |

Суров hex има само в `:root`; компонентите ползват `var()`. `color-scheme: dark` на `:root` + `<meta name="color-scheme" content="dark">` за нативно тъмни form контроли.

## Component inventory

Header (sticky, mono nav, hamburger с aria-expanded/Escape) · status chip · reticle graphic (4 контекста) · hero + page-head с grid фон · stat tiles · service cards (+flagship variant) · steps (01–03) · review panels с mono атрибуция · consult banner (amber рулетка вляво) · spec-sheet (dl) · specimen plate (figure) · portrait placeholder slot (dashed) · map plate с crosshair · FAQ `<details>` панели · booking form (тъмни инпути, amber focus ring, custom select chevron, accent-color checkboxes) · success status panel · CTA band с corner ticks · emergency band · footer (3 колони + „← Всички дизайн направления") · fixed mobile action bar (≤720px).

## Differentiation note

**The exploration's dark option — warm amber, deliberately opposite to the existing cool-teal drafts.** Нула teal/cyan/blue/green, без glassmorphism, без neon glow — топла тъмнина и месинг вместо студено стъкло.

## Porting notes

Всичко живее в `styles.css` (tokens → components); за светла тема се пренаписват само `:root` стойностите. Phase 2: формата се закача към Web3Forms (маркерът с access_key е в коментар над `<form>` в contact.html); адресът е временен (ремонт) — всички места са маркирани с `<!-- PLACEHOLDER -->`.
