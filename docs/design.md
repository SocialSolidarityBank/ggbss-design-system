# BSS Design System (edu-based)

Together We Build the World — Social Solidarity Bank. This document consolidates the design system established in the edu service.
Tokens, components, and rules are included so the same system can be applied to other pages.

---

## 1. SSOT (Single Source of Truth) Principle

- **Token SSOT = `bss-vault/web/app/_v2/tokens.css`.** All color, type, spacing, radius, shadow, and gradient variables originate in this file.
- **edu / data app pages**: import `tokens.css` directly. (No local copies allowed.)
- **Infra dashboard** (`/infra`): now a **real React page**, not a statically synced HTML file. The auth-gate server component `web/app/infra/page.tsx` renders the body client component `web/app/infra/InfraDashboard.tsx` inside the shared `AppHeader`/`AppFooter`.
  - Styles inherit `tokens.css`/`globals.css` as-is; page-specific component CSS lives in `web/app/infra/infra.css` with all selectors scoped under `.infra`.
  - Dark mode and the 1640 max-width are automatically inherited from the root layout + global tokens. No inline token blocks, `TOKENS` markers, or generator scripts (no post-edit regeneration step needed).
  - To change an infra color, edit only `tokens.css`; the change reflects on `/infra` immediately (shared tokens).

---

## 2. Tokens

### 2-1. Color

| Token | Value | Purpose |
|---|---|---|
| `--c-primary` | `#006CB7` | Brand primary. Section headings, links, emphasis |
| `--c-primary-active` | `#338BC9` | primary active/hover variant |
| `--c-dark-blue` | `#26257C` | Brand secondary |
| `--c-dark-blue-active` | `#3D3CA0` | dark-blue variant |
| `--c-sky` | `#58C5FF` | Sky accent (callouts on dark backgrounds, footer brand name) |
| `--c-sky-light` | `#CDEAFF` | Light sky (badge/chip background, gradient end color) |
| `--c-ink-deep` | `#0A1E33` | Darkest text + dark section/footer background |
| `--c-ink` | `#1A1B1F` | Body ink (rarely used) |
| `--c-body` | `#454745` | Default body text |
| `--c-grey` | `#7B7875` | Secondary text, captions |
| `--c-light-grey` | `#ECF0F3` | Light section background, input fill |
| `--c-canvas` | `#FFFFFF` | Default page background |
| `--c-positive` | `#00A775` | Success/positive |
| `--c-warning` | `#FAA41A` | Warning |
| `--c-negative` | `#F16A26` | Danger/caution (notice, etc.) |

Line (border) tokens:
`--c-line-soft: rgba(10,30,51,0.12)` (hairline divider),
`--c-line-default: rgba(10,30,51,0.20)`,
`--c-line-hover: var(--c-ink-deep)`,
`--c-line-focus: var(--c-primary)`.
Inverted (dark background): `--c-line-*-inverted`.

### 2-2. Type Scale (font & tracking)

- **Font**: Korean/general `--ff` = Pretendard(Variable), Latin/numeric `--ff-en` = Satoshi.
- **Tracking**: `--tracking: -0.01em` (applies to both Korean and Latin). Use `letter-spacing: 0` where monospace-style spacing is needed (numbers, IPs, domain names).
- **Scale tokens**: 16 / 18 / 27 / 40 / 56 / 64.

| Token | size / weight / line-height |
|---|---|
| `--fs-h1` | 64 / 800 / 1.15 |
| `--fs-h2` | 56 / 700 / 1.18 |
| `--fs-h3` | 40 / 700 / 1.25 |
| `--fs-h4` | 27 / 700 / 1.35 |
| `--fs-body` | 18 / 400 / 1.7 |
| `--fs-body-strong` | 18 / 600 / 1.7 |
| `--fs-caption` | 16 / 400 / 1.6 |
| `--fs-button` | 16 / 600 / 1.5 |

**Actual usage patterns**:
- Hero H1: 56 / 800 (mobile `clamp(34px, 7.5vw, 56px)` + `word-break: keep-all`)
- eyebrow (label above heading): 16 / **400 normal** / `--c-primary` — **bold forbidden**
- Section heading (h2): 27 / 800 / **`--c-ink-deep`**
- Card heading (h3): 21 / 800 / **`--c-ink-deep`**
- Sub-heading (h4, study cards, etc.): **20** / 800 / **`--c-ink-deep`**
- Minor heading (h5): 16 / 800 / **`--c-ink-deep`**
- Body/lead: 18 / 400, `--c-body`
- Table/comparison label (dt): **15 / 700 / `--c-ink-deep`** (one step smaller and lighter than body 16/bold — for size/weight contrast)
- Caption / table cell / FAQ answer: 16
- Badge/chip: 14~15 (floor raised from 13 → 14, 2026-06-19)

> **Minimum font size = 14px (global floor, decided 2026-06-19).** No text below 14px anywhere — labels/meta/badges/chips bottom out at `--fs-tagline` (14), body text at `--fs-caption` (16). 12/13px is off-scale and forbidden. Enforced (warning) by `web/.stylelintrc.json` over `app/**`. Pre-existing sub-14 in dense dashboards (`/data`, `/self-test`, `/infra`) and the design-system demos (`app/design/**`) are tracked as a "보류" backlog (forcing 14 risks breaking dense layouts) — clean up per-page with visual verification, or annotate genuine exceptions with `stylelint-disable` + reason.

> **Heading color = ink-deep by default.** All headings (h2~h5) use `--c-ink-deep`. `--c-primary` (blue) is for links, interactions, and emphasis text only — **never for heading color**.

### 2-3. Spacing `--sp-*`

`xs 4 · sm 8 · md 12 · lg 16 · xl 24 · 2xl 32 · 3xl 48 · 4xl 64 · 5xl 96 · 6xl 128 · 7xl 160` (px).

### 2-4. Radius `--r-*`

`xs 4 · sm 6 · ctl 8 · md 10 · lg 12 · xl 16 · 2xl 20 · pill 9999` (px, Geist alignment). Cards lg(12), tables md(10), controls (button·input·select) ctl(8), true pills·avatars pill.

### 2-5. Shadow `--sh-*`

- `--sh-soft`: `0 1px 3px rgba(10,30,51,.04)` — card hover
- `--sh-hero`: `0 2px 8px …, 0 8px 24px …` — hero/large surfaces
- `--sh-full`: `0 4px 16px rgba(10,30,51,.08)` — dropdowns/tooltips/toasts

> **`--shadow-md`/`--shadow-lg` are not tokens.** They are not defined anywhere; using them produces no shadow. Use `--sh-soft` for card hover, `--sh-full` for dropdowns/overlays.

### 2-6. Gradients

LIGHT × LIGHT only. Gradients between primary/dark-blue/ink-deep are forbidden.
- `--gr-wash-soft` white → light-grey
- `--gr-wash-sky` white → sky-light
- `--gr-wash-cool` light-grey → sky-light
- `--gr-wash-diag` 135° white → sky-light
- `--gr-wash-hero` sky-light → canvas (dedicated hero wash token for the page top; dark mode auto-overrides to `#102a44 → canvas`)

**Hero wash**: apply `var(--gr-wash-hero)` as `no-repeat / 100% 520px` on the page-top background so only the upper area fades from sky blue to white (dark: deep navy to canvas). The `/docs` wash wrapper (`.docsWash::before`) pulling behind the header (73px) is the canonical example.

### 2-7. Additional Tokens (product audit · 2026-06-08)

Values found in use across data·infra·business-map·home that were absent from §2. Promoted from ad-hoc mixes to named tokens.

- **primary/sky alpha tints** — `--c-primary-a08` `rgba(0,108,183,.08)` (hover), `--c-primary-a12` `.12` (active), `--c-sky-a18` `rgba(88,197,255,.18)` (pill-sky), `--c-positive-a12` `rgba(0,167,117,.12)` (chip-call). Used in: data filter/card, infra pill·chip, home nav.
- **Category chart color scale** (SSOT = `web/app/data/categories.ts`) — SVG `fill` cannot use `var()` so hex values are hardcoded, but **all map to token values**: light `#006CB7·#58C5FF·#26257C·#0A1E33·#7B7875`, dark `#338BC9·#58C5FF·#CDEAFF·#ECF0F3·#9aa3ad`. Shared by charts, legends, and tags. → Dark grey `#9aa3ad` is outside the palette → recommend formalizing as `--c-grey-bright`.
- **Header height `--header-h: 73px`** (confirmed — `globals.css`. AppHeader `.row` 72 + bottom border 1). Used as the reference for wash pull-up behind the header (`/docs .docsWash`), and for sticky sidebar `top` calculation. ⚠️ data `.barWrap` and business-map `.ctrl-bar` still hardcode `top: 72px` → replacing with `--header-h` is a pending consistency item.
- **Transition `--t-quick: 0.2s ease`** (`globals.css`). Standard token for fast state transitions on color, background, border, etc. New components must use this token for hover/focus transitions.
- **Control radius `--r-ctl: 8px`** — standard for form controls (button·input·select, etc.). Formally included in the §2-4 radius scale (Geist alignment, promoted to a global token).
- **Off-scale type (stat numbers)** — data stat `34` / card value `38` (tabular-nums, large-number-only) are outside the scale (16/18/27/40/56/64) → recommend adding `--fs-stat: 34`, `--fs-stat-lg: 38`. business-map sub-headings at 20/21/22 — consider absorbing into 27 (decision pending).

---

## 3. Component Catalog

Each entry: purpose + key CSS.

### Header (`.bar`)
- **Purpose**: Global top navigation, shared across all services. Sticky, semi-transparent + `backdrop-filter: blur` frosted glass, bottom hairline. (Source: `AppHeader.tsx`)
- **Layout**: `.bar` > `.row` = logo (`.logo` → portal, `/logo-bss.png` 32px) + desktop nav (`HeaderNav`) + account slot (`.account`). `max-width: var(--content-max)`, horizontal `--chrome-pad`.
- **Navigation**: Desktop uses a **cascading flyout** (`HeaderNav` — step-by-step side panels, `›` caret. See §3C); mobile uses a hamburger drawer + recursive accordion (`MobileNav`). Data source: shared `SITE_LINKS` recursive tree.
- **Account slot (`.account`)**: `ThemeToggle` + state-dependent — signed-in: `.signOut` (sign-out outline pill) + `.avatar` (circular badge with first letter of email). Signed-out: `.login` (outline pill → `/login`, fills primary on hover).
- **Theme toggle (`ThemeToggle`)**: Light/Dark segment pill in the account slot. Desktop `.account`, mobile drawer bottom (`.drawerTheme`). On click: immediately updates `<html data-theme>` + persists to cookie (`theme`, `.ggbss.or.kr` domain) + dispatches `themechange` event. Details in §5.

### Footer (`.footer`)
- **Purpose**: Site-map footer below all pages. Both modes use the page background — the top hairline alone separates it.
- **Light mode**: Background `var(--c-canvas)` — **same as the page background; a separate grey surface is forbidden** (decided 2026-06-12). Top hairline `var(--c-line-soft)`, column heads `var(--c-ink-deep)`, links/sub text `var(--c-grey)`, hover `var(--c-primary)`, copyright `var(--c-grey)`. Logo: colored CI (`CI.png`).
- **Dark mode**: Background `var(--c-canvas)` (`#0a1622`), top 1px white hairline `rgba(255,255,255,0.18)`, all text `color-mix(#fff …)` tones (unchanged from prior dark footer). Logo: white CI (`CI_white.png`).
- **Layout**: `.inner` flex space-between, `max-width: 1640`, `padding: 96px var(--chrome-pad) 16px`. Theme-switching via `:global(html[data-theme="dark"])` overrides in `AppFooter.module.css`.

### Button (`.btn`) — global default
- **Purpose**: Base variant for all action buttons. (e.g., Apply, Login, Logout)
- **Default = outline**: `background: transparent` + `border: 1px solid var(--card-border)`, text `--c-ink-deep` 700, `border-radius: var(--r-ctl)` (8px, Geist control — not pill), `height: 40px`, `padding: 0 22px`.
- **hover = primary fill**: `background: var(--c-primary)` + `border-color: var(--c-primary)` + text `#fff`.
- **focus-visible**: `outline: 2px solid var(--c-primary)`.
- New buttons use this `.btn` as the base and add only layout (flex, etc.). **Do not create solid (filled) buttons as the default.**
- **Solid CTA variant `.btn-solid` (D3 formalized)**: For a **single** primary action only, `.btn.btn-solid` — from the default state `background: var(--color-primary)` + text `var(--color-white)`, hover `var(--c-primary-active)`. Reuses existing tokens (no new tokens), dark-safe (`--color-white` re-anchored to #fff). Formally registered in globals.css. The rule "do not make solid the *default*" still holds (one solid CTA per page principle).

### Card (`.card`, `.ov-item`)
- **Purpose**: Content container.
- **Key**: `background: var(--card-bg)`, `border: 1px solid var(--card-border)`, `border-radius: 16px`, `padding: 28px 24px 32px` (bottom +4; see Korean optical correction below). Hover: `border-color: var(--c-sky)` + `--sh-soft`.
- **Korean optical bottom-padding correction (rounded box)**: Korean script has no descenders, so the text block sits toward the top of the line-box; with symmetric padding the **top appears wider and the bottom narrower**. For rounded cards/boxes, give **bottom padding 4~6px more than the top** (left/right stay symmetric). Applied to: `.card`/`.facCard` `28 24 → 28 24 32` (+4), `.studyCard` (tall card) `32 → 32 32 38` (+6), tables/lists where the last row touches the card bottom (`.compareCardRow:last-child`) get bottom +4.

### Floating Capsule CTA (`.floating-cta`) — fixed page-bottom nav+apply
- **Purpose**: Persistent section navigation + apply button on long landing pages. (Based on edu page)
- **Key**: `position: fixed; bottom: var(--cta-gap)` (desktop 40 / mobile 24); `left:50%`, `width: min(800px, calc(100% - 32px))`, **`border-radius: var(--r-xl)` (16px — rounded box, same family as buttons/cards; pill `9999px` is forbidden** — changed 2026-06-12), semi-transparent + `backdrop-filter: blur(16px)` (background `color-mix(in srgb, var(--bg) 66%, transparent)`), `--sh-full` family shadow, `z-index: 70`.
- **Alignment**: Desktop: links through the apply button are **evenly spaced + center-aligned as a group** (`.row gap == .links gap` = **36px** — widened 28→36, 2026-06-12). Apply button uses the global `.btn`.
- **Mobile (≤720)**: Links scroll horizontally (`overflow-x:auto` + edge mask fade on both sides); **apply button is pinned to the right end (always visible)**.
- **Stops above footer (required)**: To prevent the capsule from covering the footer, client JS calculates `lift = max(0, innerHeight − footer.top)` on every scroll/resize/`ResizeObserver(body)` event and applies `transform: translate(-50%, calc(-1 * var(--cta-lift)))` to lift it up — the capsule bottom always rests at **`--cta-gap` above the footer** (never below it). Update the handler **directly** (no rAF — rAF pauses in background tabs).
- **Parked spacing balance**: Give the last section (e.g., FAQ) `padding-bottom` equal to the capsule height + top/bottom balance margin (`≈ capH + 2×gap`) so that when parked, the gap above (content) and below (footer) are roughly equal. The footer's own `padding-bottom` is its normal value, unrelated to the capsule.

### Hero (`.hero`)
- **Purpose**: Page-top title area.
- **Key**: `padding: 104px 0 80px`, gradient wash (§2-6), eyebrow 16/**400** primary + H1 56/800 (mobile clamp) + lead 18 body. **No `<br>` in lead text — let the container width control line breaks naturally.**

### Section (`.section`)
- **Purpose**: Body content block.
- **Key**: Container `max-width: var(--content-max)=1640px` (`.container`, same max-width as header/footer). Full-width content uses `.reading { max-width: none }`. Between sections: **symmetric `padding: 80px 0`** + 1px hairline — the spacing above and below every section divider must be equal (see §4 divider symmetry rule). Section title `.section-title` 27/800 **`--c-ink-deep`**.
- **Horizontal edge padding — uniform across all regions**: Desktop uses `--chrome-pad` (`clamp(24px, 3vw, 48px)`) so header, body (`.container`), and footer share the same left/right margin. **Mobile (≤640px): all three use `36px` left/right** so logo, body, and footer left-edges align exactly (`.container`, `AppHeader .row`, `AppFooter .inner` all 36px).

### Table (`.table-card` — edu sessionsTable)
- **Purpose**: Row data (domain ↔ server, etc.).
- **Key**: Card-style container (radius 12, `overflow-x:auto`). `thead th` background: primary 12% tint (`color-mix(in srgb, var(--c-primary) 12%, transparent)`), 16/800. Cells 16, row hover `rgba(10,30,51,.02)`. In-row expansion (DNS details): custom JS `.dns-detail-content` max-height transition.

### Matrix (`.docsMatrix` — docs 본문 2축 비교표)
- **Purpose**: 가로 헤더행 × 세로 라벨열 2축 비교(예: edu docs "시작 메뉴"). docs 본문의 `매트릭스::` 지시어 + 마크다운 표를 `lib/docs.ts` 가 `.docsMatrix` 그리드로 변환. 스타일은 `app/docs/docs.module.css`.
- **Key**: 일반 표(th/td) 양식 — 바깥 아웃라인 없이 `gap:1px` + 컨테이너 `--c-line-soft` = 안쪽 격자선만. 가로 제목행·세로 제목열·코너 = 사이트 일반 표 `th:first-child` 와 같은 옅은 틴트, 데이터 셀 = `--c-canvas`(td). 헤더는 굵게 + **좌측정렬**, 텍스트색은 `--c-ink-deep`(테마 적응). 코너(1행 1열)는 **비움**(`매트릭스::` 축 라벨 생략 — 위 섹션 제목과 중복 방지).
- **함정(필독) — 반투명 틴트 금지**: 매트릭스 셀은 격자선 컨테이너(`--c-line-soft`) 위에 놓이므로, 일반 표처럼 *반투명* 틴트(`color-mix(… 3%, transparent)`, 선언값 `…/0.03`)를 쓰면 격자선이 배어나와 일반 표보다 진해 보인다(dev-tools 선언값은 동일해 눈치채기 어려움). 반드시 **불투명** 틴트 `color-mix(in srgb, var(--c-ink-deep) 3%, var(--c-canvas))` 로 합성을 셀 안에서 끝내야 일반 표 첫 열과 렌더가 일치한다(라이트 `rgb(248,248,249)` / 다크 `rgb(17,29,41)`, getComputedStyle 합성 계산으로 검증). 규칙: solid 불투명 배경엔 고정색 텍스트, alpha 틴트엔 테마 적응색(다크모드 글자 사라짐 방지).

### Study Card + Accordion (`.vendor-acc` — vendor details)
- **Purpose**: Collapsible per-vendor details (contact info, etc.).
- **Key**: Native `<details>`. Summary: name (`.va-name` 21/800) + tag (`.va-tag` pill) + external site `.va-link` + `+/×` icon (`.faq-icon`). Body `.study-detail`: top hairline + `.info-list`/`.row` contact rows.
- **+/× icon**: 28px circle with sky-light background, two bars via `::before`/`::after` forming a `+`. On `details[open]`: background primary + `rotate(45deg)` → `×`.

### FAQ Accordion (`.faq-acc` — situation-based guide)
- **Purpose**: Question/answer collapsible.
- **Key**: Native `<details>`. Summary 18/800 + `.faq-icon` (+/×, same as above). Answer `.faq-answer` 16 body, `strong` is primary.
- **2-column layout**: When splitting into two columns for wider layouts, **`columns` (CSS multi-column) is forbidden** — expanding an item causes items to redistribute across columns and break alignment. Instead use **two independent columns** (each grid cell is a `flex-column` stack with items pre-distributed to left/right), so expanding an item shifts only its own column while the other stays fixed. Single column on mobile.

### Badge/Tag Pill (`.pill`, `.va-tag`, `.chip`)
- **Purpose**: Status/category labels (`.pill-blue/sky/out/amber/grey`), action chips (`.chip-copy/open/call`).
- **Key**: `border-radius: 9999px`, small text (13~14), `letter-spacing: 0`. Chips handle copy/open/call actions.

### Tooltip (`.term`)
- **Purpose**: Hover/focus explanation for technical terms.
- **Key**: Dashed underline (`1px dashed var(--c-sky)`) + primary text, `cursor: help`. `.tip` speech bubble: ink-deep background / white text, `--sh-full`, shown on hover/focus-within.

### Notice (`.notice`)
- **Purpose**: Informational callout (low-emphasis inline notice). For warning/error intents use the 3-intent Banner set (info / warning / error).
- **Key**: `--c-sky` 10% background + `--c-primary` 28% hairline border, radius 16, `strong` is primary (sky in dark mode).

---

## 3B. Additional Components (product audit · 2026-06-08)

§3 covers edu only. These components are **actually used but absent** in products beyond edu (data·infra·business-map·home·login·coming-soon). Each entry: purpose + key + source. (Showcase-only items — carousel, option-card, glassmorphism, etc. — are intentionally excluded.)

### Form — input / label / validation (`.input`, `.label`, `.error`, `.notice`)
- **Purpose**: Input forms for login, filters, etc. (Source: `web/app/login/page.module.css`)
- **Key**: `.input` line style — `padding 14px 16px`, `font-size 16px` (≥16 required), `border 1px var(--card-border)`, focus: `outline 2px var(--c-primary)` + border primary. `.error` validation errors **must use `--c-negative`** (currently `#c33` = violation). `.notice` informational: primary 8% background. Radius must use §2-4 tokens (currently 10/18 are off-scale → needs alignment).
- Rebuilt version already exists at `web/app/design/components/input` — now formally registered in SSOT.

### Select — custom chevron (`.sel`)
- **Purpose**: Unified select with native arrow removed. (Source: data `page.module.css:128`)
- **Key**: `appearance:none` + `background-image: var(--chevron)` (inline SVG) `right 13px center`, `padding-right 40px`, height 40px, focus: `inset 0 0 0 1px var(--c-line-focus)`. Light/dark automatic.

### Tab — underline (`.tabBtn`/`.tabOn`)
- **Purpose**: View switching (dashboard/table). (Source: data `:63`)
- **Key**: `border-bottom: 2px solid transparent` + `margin-bottom:-1px` (overlaps container line); active `.tabOn` = primary text + primary underline. 16/600.

### Filter/Search Bar (`.bar`/`.search`/`.reset`)
- **Purpose**: Combined search + multi-select + select + reset toolbar. (Source: data `:96`)
- **Key**: `flex; flex-wrap:wrap; gap --sp-sm`, all controls height 40px, sticky `top: var(--header-h)`. `.reset` is `margin-left:auto` (always right-aligned). Floats above the wash with no wrapping box.

### Data Grid — sort & column reorder (`TableView`)
- **Purpose**: Analytical table (sort, column reorder, row selection). **Distinct from** §3 `.table-card` (edu simple read table). (Source: data `DataExplorer.tsx:547`, css `:770`)
- **Key**: Header-click sort (↕/▲/▼ `.sortBtn`), column left/right move buttons (`.moveBtn`, persisted to localStorage), row-select checkboxes, right-aligned numbers (tabular-nums). Wide tables expose a **top-synced scrollbar** (`.topScroll` 14px, synced to body via ResizeObserver).

### KPI/Stat — strip + card (`.statStrip`, `.cards/.card`)
- **Purpose**: Large numeric indicators. (Source: data `:244`, `:648`)
- **Key**: `.statStrip` flex + `.statDiv` 1px divider, `.statNum` = Satoshi 800 `34px` tabular-nums `--c-primary-active` (readable in dark), label 16/800 ink-deep. `.cards` 3-up grid (`--sp-xl` gap), `.cardValue` `38px` 800 ink-deep, card radius `--r-sm(8)`.

### Drawer/Sheet + Overlay (`.drawer`/`.ov`)
- **Purpose**: Right-side slide-in detail panel. §3 has no modal/sheet. (Source: data `:534`, `DataExplorer.tsx:1088`)
- **Key**: `.ov` scrim `rgba(10,30,51,.35)` `inset:0 z-index:20`; `.drawer` `position:fixed; right; top`, `width min(560px,94vw)`, `--sh-full`, `padding --sp-xl`, `role=dialog aria-modal`, Esc to close. `.close` top-right pill.

### Toast (`.toast`)
- **Purpose**: Temporary bottom notification (copy confirmation, etc.). (Source: infra `infra.css:528`)
- **Key**: `fixed; bottom:36px; left:50%`, ink-deep background / canvas text, `--r-md`, 14/600, `--sh-full`, `cubic-bezier(.4,0,.2,1)` slide, `.show` toggles opacity+translateY, auto-dismisses after 2s, `pointer-events:none`.

### Semantic Tag Taxonomy (`.t-*`, `.b_*`)
- **Purpose**: Classification/hierarchy labels. Extends §3 `.pill/.chip` with a **semantic color set**. (Source: business-map `:265`, data `:469`)
- **Key**: Pill shape (`--r-pill`, 14/600, `letter-spacing:0`). Hierarchy expressed via **color recipe**: `.t-gov` (primary 12% tint) · `.t-csr` (grey 14%) · `.t-self` (dark-blue + border) · `.t-new` (solid primary = highest emphasis). All dark-safe (dark text: sky). data record tags (`.b_report/.b_ledger`) currently use raw hex → needs token mapping.

### Chart — bar + legend + bar-row (`BudgetBarChart`, `.legend`, `.w-*`)
- **Purpose**: Data visualization. (Source: data `charts/BudgetBarChart.tsx`, business-map `:309`)
- **Key**: recharts horizontal bar, cell color = §2-7 category scale, custom tooltip (ink-deep surface). Lightweight variant = **bar-row** (`.w-label 220px` + `.w-track 8px` + `.w-fill` scaleX animation (scroll-in, respects reduced-motion) + `.w-val 64px` tabular). **Legend** = color dot (`.catDot/.leg-pip` 9~10px) + label, synchronized with chart colors.

### Chip/Pill Variants + In-Table Accordion (infra)
- **Purpose**: Status color variants + action chips + in-row expansion. (Source: infra `:219`, `:421`, `:230`)
- **Key**: `.pill-blue/-sky/-out/-amber/-grey` 5 colors (all token-based + dark-corrected). `.chip-copy/-open/-call` action chips (copy/open/call, 14px SVG). Row expansion `.dns-detail-content` = `max-height` transition + `.open` arrow 180° rotation (JS-based, distinct from the native `<details>` approach in §3). Code chip `.dns-code` = mono, canvas background, `--r-md`, line-soft border.

### Portal Tile (`.pc`) — apex (ggbss.or.kr home) only
- **Purpose**: Subdomain link card grid. (Source: home `index.html:43`)
- **Key**: `.portal` 4-column grid (responsive 3→2→1), `.pc` = canvas background + `--c-line-soft` border + `--r-lg` + `--sh-soft`, hover: `translateY(-4px)` + `--sh-hero` + `--gr-wash-diag` wash. Interior: `.pc-idx` (sky number) + `.pc-name` (ink-deep) + `.pc-domain` (primary) + `.pc-arrow` (circle, primary on hover). `.soon` = inactive (grey). **Tile itself is already token-aligned** — only the chrome on the same page is off-system (§4 chrome unification).

### Stub "Coming Soon" Page (coming-soon)
- **Purpose**: Stub pages for brain/manual/www. (Source: `web/app/coming-soon/` — **React route** `ComingSoonHero` → `StaticHero`)
- **Key**: `ComingSoonHero` (`"use client"`) selects per-host (brain/www/manual) copy and renders the shared `StaticHero` — **token-based alignment** (uses StaticHero). Host copy is resolved in a client `useEffect` (stays static). ※ The old off-system static `coming-soon/index.html` (raw hex, no `tokens.css` load, <16px) is a **legacy zombie** (to be retired — replaced by this app route).

### WordHero (text hero) — ⚠️ DEAD (removed)
- **Purpose**: ~~Minimal Latin-text landing~~ **unused**. Importer count 0 — `StaticHero` (no-scroll deduped hero) fully replaces it (wiki also uses `StaticHero`). `web/app/_components/WordHero.tsx` + `.module.css` were deleted in STAGE 3.
- **Key**: (Reference) Link-free Latin-word hero + tagline. **No longer live** — see `StaticHero`.

---

## 3C. Additional Components (lecture docs hub · 2026-06-09)

New components introduced in the edu `/docs` hub. Each entry: purpose + key + source. (Live demos: design.ggbss `/design/components/{doc-card,search,nav-flyout}`, `/design/patterns/{full-bleed-divider,hub-dashboard}`.)

### Doc Card (`.docCard`)
- **Purpose**: Clickable navigation card for selecting lecture documents (hub grid). (Source: `web/app/docs/docs.module.css`, `DocsHub.tsx`)
- **Key**: Vertical stack — title (17/700 ink-deep) + summary (14 grey) + meta (reading time `Nmin`, Clock icon 13px, primary/dark sky). `canvas` background + `--c-line-soft` border + `--r-lg`. Hover: `translateY(-2px)` + `--sh-soft` + primary (dark: sky) border. **Distinct from §3 `.card` (content container)** — this is a link navigation card.
- **Grid**: `repeat(auto-fill, minmax(280px, 1fr))`, `gap --sp-lg`.

### Action Card (`.actionCard`)
- **Purpose**: External action link (enrollment, self-assessment, etc.). (Source: same as above)
- **Key**: Horizontal `space-between` — label (16/600 ink-deep) + `↗` (ArrowUpRight 18px). Hover: card lifts + icon `translate(2px,-2px)`. Link data sourced from `site-nav.ts` SSOT (no hardcoding).

### Hub Search (`.hubSearch`)
- **Purpose**: Client-side hub document search (title · summary · body). (Source: `DocsHub.tsx`)
- **Key**: `flex` — Search icon (18px grey) + `input[type=search]` (16px, no border, transparent) + result count (13 primary/dark sky). Wrapper: `canvas` + `--c-line-soft` border + `--r-lg`. `focus-within`: primary (dark: sky) border + `0 0 0 3px` ring. **Distinct from §3B `.bar/.search` (data filter toolbar)** — standalone search with result count.

### Lecture Docs Hub Layout (`.hub`)
- **Purpose**: `/docs` landing dashboard — head + search + per-group card grids (`Education`) + action links (`Educational Materials`). (Source: `DocsHub.tsx`, `app/docs/page.tsx`)
- **Key**: Vertical stack (`gap --sp-2xl`), `max-width: var(--content-max)`. Data is **computed server-side (`page.tsx`) from `docsNav` + MD files and injected as props** (SSOT; no client-side hardcoding). Section labels use uppercase tracking (`SECTION` style).

### Full-Bleed Divider (`.hubRule` + wrapper `.docsWash`)
- **Purpose**: Horizontal rule that extends to the viewport edge, breaking out of the content padding.
- **Key**: `width: 100vw; margin-left: 50%; transform: translateX(-50%)`. **Safety wrapper required** — parent must have `overflow-x: clip` (absorbs the scrollbar-width overflow of 100vw, prevents horizontal scroll) + `isolation: isolate` (isolates wash z-index). `clip` does not create a scroll container, so it does not break sticky sidebars in the body. (Source: `docs.module.css .hubRule`/`.docsWash`)

### Cascading Flyout Navigation (Header)
- **Purpose**: Global header navigation shared across all services. Items with children show a caret (▾/›); on hover/focus, a panel slides out to the side step by step (amplemarket/retool style, recursive, unlimited depth). (Source: `HeaderNav.tsx`, `site-nav.ts`, `AppHeader.module.css`)
- **Data**: `SiteChild` recursive tree (`children?: SiteChild[]`). **Nodes with `href` = pages (`<a>`); nodes without = categories (`<button>`, no navigation — expands children only).** `authOnly` nodes are hidden when signed out; `visibleTree()` filters them.
- **State**: `openPath` = chain of open node ids (`"edu/0/0"`). `chainOf(id)` opens ancestors and closes siblings and deeper branches (one branch at a time). Hover-intent: opens immediately on enter, closes with a 140ms delay on leave to allow diagonal mouse movement.
- **Surface**: `.flyoutPanel` semi-transparent + `blur(16px)` + `--sh-full`, 232px wide. `.flyoutRow` transparent → on open: `.flyoutRowOpen` (primary 9% tint + primary label/caret). Label 15/600, single label unified (#51 — tagline/`.flyoutDesc` removed). Sub-panel `.flyoutSub` cascades to the right at `left:100%`.
- **Responsive**: Header = flyout, mobile = accordion (`MobileNav`), footer = leaf-flattened. All share the same `SITE_LINKS` tree. (Live: `/design/components/nav-flyout`)

---

## 4. Usage Rules (Guardrails)

- **Use only defined tokens**: Colors, fonts, backgrounds, spacing, radius, and shadows must use the tokens above. Arbitrary hex or arbitrary px values are forbidden (add a token first if one is missing).
- **Reuse defined components**: Combine from the catalog above instead of improvising new patterns.
- **Heading color = ink-deep by default**: Headings (h2~h5) use `--c-ink-deep`. `--c-primary` is for links, interactions, and emphasis only (never heading color). eyebrow uses **normal (400)**.
- **Button default = outline (`.btn`)**: Fills primary on hover. Do not create solid buttons as the default.
- **Rounded box bottom padding +4~6 (Korean optical correction)**: Korean script has no descenders, so symmetric padding makes the top appear wider than the bottom. Rounded cards/boxes get bottom padding 4~6px more than the top (left/right stay symmetric). See §3 card for details.
- **Dividers must never stop mid-screen (strict — re-enforced 2026-06-12)**: A divider line that ends in the middle of the screen reads as broken UI.
  - **Horizontal layout dividers run full-bleed**: never put the hairline on a `max-width` container (it cuts off at 1640 on wide screens). Put the border on a full-width wrapper with the constrained content inside (canonical: data `.tabsWrap` > `.container`, docs `.tabBar` > `.tabBarInner`), or use the 100vw `.hubRule` pattern (§3C) inside an `overflow-x: clip` wrapper.
  - **Vertical sidebar↔body dividers are forbidden entirely**: a sticky sidebar's `border-right` ends where its content ends — the line dangles mid-screen. Separate sidebar and body with whitespace (grid gap) only. Sidebar-internal title underlines (lines that stop at the sidebar edge) are also forbidden — express hierarchy with weight and spacing.
  - **Allowed short lines**: IDE indent guides (span exactly their nested group), in-content reading-column rules (markdown `hr`, table row lines, accordion item lines inside their column), and lines fully enclosed in a card.
  - Violations fixed 2026-06-12: docs/design sidebar `border-right` + `.sidebarHeader` underline removed; docs `.tabBar` hairline moved to a full-width wrapper.
- **Numbering/icon alignment = container-based, not text-based (strict — decided 2026-06-12)**: A number badge or icon that labels a list row / step card must be **vertically centered against the row container (div)** — never aligned to the first text line or baseline. Use `top: 50%; transform: translateY(-50%)` for absolute badges, or flex `align-items: center` on the row. Keep **at least 20px of gap** between the badge and the text block (e.g., edu pipeline: badge 28px at `left: 18px` + row `padding-left: 68px` = 22px gap).
- **Divider symmetric spacing (decided 2026-06-12)**: The whitespace **above and below every horizontal divider must be equal** — section hairlines use symmetric `padding: 80px 0`, accordion item lines use equal padding on both sides (e.g., FAQ summary `20px 0` / answer bottom `20px`). An asymmetric gap around a line reads as a layout bug.
- **List bullets = one global token (`--bullet-color`) (decided 2026-06-12)**: Every list bullet — pseudo-element `•` and native `::marker` alike — uses the single alias `--bullet-color` (light: `--c-primary`, dark: re-anchored to `--c-sky` in globals.css). Per-page bullet colors are forbidden. Prefer the shared `•` pseudo-element pattern (`list-style: none` + `li::before`) so glyph size also stays uniform; native `disc` markers render a different glyph and must not be mixed with `•` in the same page.
- **No middle-dot abuse in running text (decided 2026-06-12)**: Do not use `•`/`·` as a stand-in for words in body text — write dates and ranges out (e.g., `2026년 6월 ~ 12월`, never `2026 · 6–12월`). Middle dots are allowed only for compact same-kind enumeration inside chips/labels (e.g., `김·이·박`).
- **No one-sided border on a rounded box (strict)**: Any box with a `border-radius` must use a full `1px solid` border on all four sides (it follows the radius) — never a single-side accent (`border-top` / `border-left` / etc.) on a rounded box. A straight one-sided line cuts across the rounded corner and reads as broken. For an accent, use a full hairline + `--sh-soft` shadow, or a tag/pill that carries the color. One-sided borders are allowed ONLY as structural separators on non-rounded edges (IDE-style indent `border-left` guide, section-top hairline, table-cell `border-bottom`) and as two-edge borders that draw a glyph (checkmark, chevron). (Sidebar `border-right` was removed from this exception list 2026-06-12 — see the full-bleed divider rule below.)
- **Horizontal edge padding alignment (header · body · footer identical)**: Desktop: `--chrome-pad`; **mobile (≤640px): `36px`** left/right for header, body (`.container`), and footer so their left edges align exactly. Do not define per-page/component horizontal padding independently. See §3 section for details.
- **Max-width = 1640 global rule**: All app pages (edu·data, etc.) use `--content-max: 1640px` — same as header/footer max-width. No per-page widths (e.g., old data 1320). Even dense multi-column layouts must fit within 1640.
- **Dark mode via global tokens**: Handle dark mode through `[data-theme="dark"]` token overrides, not per-component recoloring. Use `:global(html[data-theme="dark"]) .x` scoped rules only for unavoidable surfaces. Details and rules in §5.
- **Nav menus**: Both header and floating use **weight 600**, chevron `strokeWidth 2.5`.
- **Fonts: Pretendard / Satoshi only**.
- **No emoji**. Use inline SVG for icons (+/× pseudo-elements, chevrons, etc.).
- **No italic**. Use weight or color for emphasis only (`em, i { font-style: normal }` enforced).
- **Gradients: LIGHT × LIGHT only**. Dark-to-dark is forbidden; depth on dark backgrounds uses flat color + shadow.
- **Infra dashboard (`/infra`) is a real React page**: `page.tsx` (auth-gate server component) + `InfraDashboard.tsx` (body) + `infra.css` (`.infra` scope). It inherits global tokens, dark mode, and 1640 max-width automatically — edit only `tokens.css` (no generator/sync step). See §1.
- **Chrome (header·footer) unification (decided 2026-06-08)**: All services use **one token-based chrome**. React apps use `.bar` (header) / `.footer` (footer) (§3). **The handcrafted `.bssc-*` chrome on static sites (home·coming-soon) is a unification target** — currently using raw hex (`#0a1e33`·`#006cb7`·`#5b6573`·`#e6e9ee`), `max-width:1180` (not 1640), solid login button, mobile nav 13px = all violations. Static sites must also load `tokens.css` and follow color, max-width (1640), ≥16px, and outline-button rules. → **Follow-up implementation work** (static site update + redeploy).
- **Solid CTA variant `.btn-solid` (D3 formalized — decided 2026-06-11)**: Outline (`.btn`) stays the default, but **one primary action** may use `.btn.btn-solid` (primary fill + white text, hover = active tone) — formally registered in globals.css (see §3 Button). Migrating the call sites (home/coming-soon `.bssc-login`, claude.design `.btn-primary`) is W2. A sky variant on dark backgrounds (`.btn-sky`) is to be added in W2 if needed after confirming call sites. The rule "do not make solid the *default*" still holds.
- **Dark mode neutral grey fill + light text forbidden (strict)**: In dark mode, combining a neutral grey fill (`--c-light-grey`) with white/light text is forbidden — this applies to surfaces, content boxes, **and also interaction states (hover/active) and inline code**. Use outline (transparent/canvas background + 1px border) or low-alpha semi-transparent tint instead. **Exceptions (keep as-is)**: ① semantic/brand color fills (primary·sky·positive·warning·negative — not grey), ② dark-mode-only code blocks (`.codeBlock`), ③ floating overlays (tooltip `.tip` — dark mode uses a dark text color), ④ color swatches/demo stages with no text. See §5-3.
- **No decorative grid in preview/placeholder backgrounds**: Do not apply decorative line grids or diagonal hatching (`repeating-linear-gradient`, `linear-gradient(... 1px ...)`) to live preview stages or image placeholder backgrounds. Use a clean flat color/canvas instead.

---

## 5. Dark Mode (Global Theme)

Light/dark toggle shared across all services. **Single token set inverted** — no per-component dark designs.

### 5-1. Behavior (no-flash · subdomain sync)
- **Storage**: Cookie `theme` (`light`|`dark`), `domain=.ggbss.or.kr; path=/; max-age=1y; samesite=lax` → preference shared across subdomains (edu·data·portal, etc.).
- **Application**: Server (`layout.tsx`) reads the cookie and sets `<html lang="ko" data-theme={theme}>` **via SSR** → correct theme from the first paint (no flash). Default: `light`.
- **Toggle**: `ThemeToggle` (client) Light/Dark segment — header `.account` (desktop) + mobile drawer `.drawerTheme`. On click: ① immediately updates `document.documentElement.dataset.theme` (smooth transition via `html,body { transition }` in globals), ② writes cookie, ③ dispatches `window` `themechange` event.
- **Client subscription**: Places that consume color via JS (e.g., `/data` explorer charts/canvas) subscribe via `MutationObserver(html[data-theme])` + `themechange` to track the current theme. Initial value comes from the SSR cookie prop for hydration consistency.

### 5-2. Dark Token Set (`tokens.css` `[data-theme="dark"]`)
Only base `--c-*` are overridden → globals.css aliases (`--bg`, `--card-bg`, `--text-main`, …) follow automatically.
| Token | Dark value | Note |
|---|---|---|
| `--c-canvas` / `--bg` | `#0a1622` | Page background |
| `--c-ink-deep` | `#ffffff` | Heading/emphasis text (white in dark) |
| `--c-body` | `#ecf0f3` | Body text |
| `--c-grey` | `#c3ccd6` | Secondary |
| `--c-light-grey` | `#1f3a59` | Dark surface tint |
| `--c-line-soft/default/hover` | `rgba(255,255,255,.10/.24/.85)` | Lines (inverted) |
| `--c-line-focus` | `var(--c-sky)` | Focus |

**Alias trap (must re-anchor)**: globals.css `--color-white: var(--c-canvas)` and the footer's `--c-ink-deep` **flip** via the override above. Re-anchor `--color-white: #ffffff` inside the dark block (for button text), and use `--footer-bg` (§3) for the footer.

### 5-3. Dark Design Rules
- **Dark text colors: white / sky (`#58C5FF`) / light-blue (`#CDEAFF`) / light-grey (`#ECF0F3`) only.** In dark mode, links and emphasis use **`--c-sky` instead of primary** (primary blue is too dark on dark backgrounds).
- **Distinguish surfaces via border/line, not fill** — in dark mode, cards use no separate light fill: `--card-bg` = background + border only.
- **Neutral grey fill boxes forbidden (strict)** — rule boxes, callouts, notes, table headers, neutral label chips, flow boxes, etc. must not use a solid grey surface (`--c-light-grey` = `#1f3a59`) with white/light text in dark mode (insufficient contrast; "AI grey box" impression). Use transparent/canvas + 1px border, or a low-alpha tint (e.g., `color-mix(... 6~12%, transparent)`). **Same rule applies to hover/active states and inline code** — use `--c-line-soft` hairline tint, not solid grey. Exceptions: brand/semantic color fills, `.codeBlock`, tooltip overlays, color swatches/text-free demo stages (see §4).
- **LIGHT×LIGHT gradients are forbidden in dark mode** — light washes (hero, etc.) must be overridden with a dark wash (e.g., `#102a44 → --c-canvas`). Depth on dark backgrounds uses flat color + lines.
- Component dark corrections follow the pattern `:global(html[data-theme="dark"]) .className { … }` in CSS modules (adds dark values without touching light values).
