# 01 — Protocol (модерно-клинична)

**One-line pitch:** Кабинетът, който работи точно — всяка линия, номер и празно поле внушават контролирана, измерима прецизност.

## Mood

Calm precision, quiet competence. Нищо декоративно, което не е правило (hairline), число или whitespace. Бял фон, 1px разчертаване, един-единствен азурен акцент. Съзнателно скъсване с текущия сайт: никакъв teal/cyan, никакъв glassmorphism.

## Target patient

Заети професионалисти (30–55), които сравняват зъболекари по сигнали за компетентност: рейтинг, квалификации, протоколи, микроскоп. Четат бързо, решават рационално, конвертират през „Запазете час" или директно обаждане.

## Key design moves

1. **Hairline-разчертани секции + номерирани микро-етикети** — всяка секция започва с 1px правило и UPPERCASE етикет с индекс („01 — Услуги", 11px, letterspacing .14em, азур).
2. **Услугите като номерирани редове** (services.html): номер | име + описание | стрелка-CTA към резервация. НЕ карти. На Начало — компактна bordered 2×3 решетка със stretched links.
3. **Hero split:** копи вляво; вдясно бордиран „резервационен панел" (1px ink рамка) с работно време, телефон, чипове НЗОК / Прием на деца / BG–EN и CTA — конверсията е първокласен обект в дизайна.
4. **Stat strip:** 4 показателя, разделени с hairlines, едри Manrope-цифри (10+ / 356 / 5.0 / НЗОК).
5. **Линкове с анимиран 1px азурен underline** (width 0→100%); картите се повдигат 2px само при hover (единствената сянка в системата е hover-сянката). Активната страница в навигацията носи постоянен 1px underline.

## Token summary

### Палитра

| Token | Hex | Роля | Контраст |
|---|---|---|---|
| `--color-bg` | `#FFFFFF` | основен фон | — |
| `--color-bg-mist` | `#F2F6FA` | панели, банери, placeholder-и | — |
| `--color-ink` | `#0F1C28` | заглавия, тъмна CTA-лента | 16.2:1 на бяло |
| `--color-text` | `#40525E` | основен текст | 8.1:1 бяло / 7.5:1 mist |
| `--color-accent` | `#0E6BA8` | акцент, бутони, kickers | 5.7:1 на бяло (AA и за 11px) |
| `--color-accent-deep` | `#0A527F` | hover, наситени линкове | 8.3:1 на бяло |
| `--color-line` | `#DCE5EC` | декоративни hairlines | декоративен |
| `--color-line-strong` | `#7F93A3` | **добавен**: рамки на inputs/checkbox | 3.2:1 (WCAG 1.4.11 non-text) |
| `--color-ink-soft` | `#31465A` | **добавен**: hairline върху тъмно | декоративен |
| `--color-inverse-muted` | `#B9C9D6` | **добавен**: вторичен текст върху ink | 10.2:1 на ink |

AA бележка: зададената палитра минава AA без корекции (бял текст върху `--color-accent` = 5.7:1). Трите добавени токена покриват случаите „контрол-рамка на бяло", „линия на тъмно" и „muted текст на тъмно", които базовата палитра не адресираше.

### Типография

- **Display:** Manrope 700/800 — заглавия, цифри, бутони; tight leading (1.08–1.15), отрицателен letterspacing.
- **Body:** Inter 400/500/600 — текст, етикети, формуляри.
- Скала: H1 `clamp(2.1rem, 5vw, 3.3rem)` · H2 `clamp(1.5rem, …, 2.125rem)` · lead `clamp(1rem, …, 1.125rem)` · микро-етикети 11px UPPERCASE `.14em`.
- И двата шрифта имат пълна кирилица (Google Fonts css2, автоматичен cyrillic subset).

### Spacing / radius / shadow

- Spacing: 4px растер, `--space-1…9` (4 → 104px); секции `clamp(56px, 8vw, 104px)`.
- Radius: `--radius-base: 3px` навсякъде (карти, бутони, inputs, чипове); `--radius-tight: 2px` за вложени изображения/фокус.
- Линии: `--line` = 1px `--color-line` (шорткът-токен за border); никакви плътни разделители, само hairlines.
- Сянка: единствен токен `--shadow-hover: 0 8px 24px rgba(15,28,40,.08)` — прилага се **само** на hover (карти, primary бутон, стрелка-CTA). В покой системата е плоска.

## Component inventory

`skip-link` · `utilitybar` (desktop: адрес + работно време + телефон) · `header` (sticky, hairline) + `brand` с монограм „К" · `nav` (hamburger <1024px, aria-expanded/controls, Escape) · `btn` (primary / ghost / inverse / sm) · `a-line` (анимиран underline) · `hero` split + `panel` (резервационен) + `chips` + `rating` · `stats` strip · `svc-grid`/`svc-card` (Начало) · `svc-rows`/`svc-row` (Услуги) · `badge` („Под микроскоп") · `steps` (hairline-таймлайн) · `photo-band` · `reviews`/`review` · `consult` банер · `faq` (details/summary с +/− икона) · `about-grid` + `cred-list` (checkmark SVG) + `frame`/`placeholder` (портрет, карта) · `infostrip` (Прием) · `contact-grid` + `info-rows` + `callout` (спешност) + `map-ph` · `form` (custom inputs, select-wrap, checkline, success) · `cta-band` (тъмна) · `footer` · `mobile-bar` (фиксирана ≤720px). Иконография: изцяло inline SVG, stroke 1.5, currentColor.

## Porting notes

Всички стойности живеят в `:root` на `styles.css` (hex само там; компонентите ползват `var()`), затова портването към build.py шаблона е механично: token-блокът се излива в шаблонните променливи, а компонентните класове (BEM-ish, без per-page overrides) се пренасят 1:1. Адресът е навсякъде маркиран с `<!-- PLACEHOLDER -->` (временен заради ремонт), формата носи Phase-2 коментар с Web3Forms ключа — двете точки за смяна при продукционен билд.
