# Handoff: Bolt — food delivery home / discovery screen

## Overview
Bolt is a food-delivery app for Lahore whose single differentiator is **speed**. This handoff
covers the first screen a signed-in customer lands on, in two forms:

- **Mobile home / discovery** (iOS, 402×874) — address + profile, category chips, a "Bolt lane"
  carousel of the fastest kitchens, a staged live-order tracker, and a restaurant list.
- **Web home / discovery** (desktop, 1360px content column) — the same information architecture
  translated to desktop conventions: sticky top nav, left filter rail, 3-across card grid.

Target branch for the work: **`dev`** on `shahzaibq12/food-delivery-mvp`.

## About the design files
The files in this bundle are **design references created in HTML** — prototypes that show intended
look and behaviour. They are **not production code to copy directly**. They are authored as
"Design Components": a single `.dc.html` file holding a template plus a small logic class, with all
styling inline. That format exists for the design tool, not for your app.

Your task is to **recreate these designs in the target codebase's existing environment**, using its
established patterns, component library, routing and state management. The current repo
(`food-delivery-mvp`) is a single static `index.html` prototype with no framework, so part of this
work is choosing the stack. Recommendation, given the repo is greenfield: **React + TypeScript +
Vite**, CSS custom properties for the tokens below, and `lucide-react` or `@phosphor-icons/react`
for icons (the designs use Phosphor). Any equivalent modern stack is fine — the constraint is that
the visual result matches, not that the code matches.

## Fidelity
**High-fidelity.** Colours, type sizes, spacing, radii, icon set and copy are all final. Recreate
pixel-accurately. Every value you need is listed under **Design tokens** and inline in the
component tables below.

Two deliberate placeholders that are NOT final:
- Restaurant/dish photography is drawn as diagonally-hatched blocks labelled `PHOTO`. Wire these to
  real image fields; keep the exact box dimensions and radii.
- Restaurant data is dummy content (12 kitchens). Replace with API data; keep the field shape.

## Design system
The visuals follow **Nocturne**, a dark, compact design system: near-neutral blue-grey ground, Inter
at weight 400–500 (never bolder than 500 for headings — hierarchy comes from size and space), 8px
base radius, and accents used as lines, marks and glows rather than large fills. Rules and dividers
are 1px hairlines; elevation on the dark ground is an edge plus ambient darkness, never stacked
shadows. Buttons are **outlined** (1px accent border on transparent), not solid-filled.

### The two-accent rule — important
The palette has two accents with **non-interchangeable jobs**:

- **Purple `#9184d9`** — brand and chrome: the logo's machine parts, wordmark, cart button, avatar,
  ratings, links, focus rings, active category marks.
- **Electric lime `#b6f21c`** (text-safe tint `#cdf765`) — **speed and time only**: the Bolt lane,
  every ETA/minute figure, the live-order tracker, the "Fastest" sort when active, the "Bolt lane
  only" toggle when on, and the logo's bolt.

If a new element expresses time-to-door, it is lime. If it is brand furniture, it is purple. Never
flood a large area with either; both stay as lines, small fills at ≤16% alpha, and glows.

## Screens / views

### 1. Mobile — home / discovery (402×874)
**Purpose:** pick a kitchen fast; see how far away an in-flight order is.

Vertical flex column on `radial-gradient(120% 55% at 50% 0%, #20233a 0%, #161826 56%)`.
Safe-area top padding 56px. Sections top to bottom:

| # | Section | Layout & spec |
|---|---|---|
| 1 | **Header row** | `padding: 56px 18px 12px`, flex, `gap: 12px`, centre-aligned. Left: 40×40 profile button, `border-radius: 12px`, `border: 1px solid #9184d9b3` (accent-700), `background: rgba(145,132,217,.12)`, `box-shadow: 0 0 18px rgba(145,132,217,.22)`, Phosphor `User` 20px in `#c9c2ec` (accent-200). Centre column (flex:1, min-width:0): brand row = 22px logo mark + "Bolt" (`font-heading` 15px/600, `letter-spacing:.02em`) + 1×11px `rgba(233,233,237,.2)` divider + address "12-C Gulberg III ⌄" (13px, `rgba(233,233,237,.6)`, single-line ellipsis); under it "Average delivery near you: 24 min" (11.5px, `#cdf765`, `margin-top: 4px`). Right: 40×40 search button, `border-radius: 12px`, `1px solid #2f3242` (divider), `background: rgba(233,233,237,.05)`, Phosphor `MagnifyingGlass` 18px. |
| 2 | **Live order tracker** | `margin: 2px 18px 14px`, `border-radius: 8px`, `border: 1px solid rgba(182,242,28,.3)`, `background: linear-gradient(100deg, rgba(182,242,28,.1), rgba(35,37,50,.5) 70%)`, `padding: 11px 12px 12px`. Top row: stage name (12.5px `#cdf765`) + " · Burger Cartel" (`rgba(233,233,237,.45)`), sub-line 11px `rgba(233,233,237,.42)` ("Two streets away · handing off at 12-C Gulberg III"), and a right-aligned "4′" (`font-heading` 20px/500, tabular-nums, `#cdf765`, `text-shadow: 0 0 16px rgba(182,242,28,.4)`). Below: 4-column grid, `gap: 6px`, `margin-top: 11px` — see **Order tracker** below. Footer row `margin-top: 7px`, 10.5px `rgba(233,233,237,.4)`, "Ordered 7:41" left / "Delivered ~8:04" right. |
| 3 | **Bolt lane header** | `padding: 0 18px 8px`, flex baseline space-between. Left: Phosphor `Lightning` 14px `#b6f21c` + "BOLT LANE" (`font-heading` 13px/500, `letter-spacing:.08em`, uppercase). Right: "under 25 min, guaranteed" 11.5px `rgba(233,233,237,.45)`. |
| 4 | **Bolt lane carousel** | Horizontal scroll (scrollbar hidden), `gap: 10px`, `padding: 0 18px 16px`. Cards 150px wide, `border-radius: 12px`, `border: 1px solid rgba(182,242,28,.28)`, `background: linear-gradient(160deg, rgba(182,242,28,.09), rgba(30,32,43,.88))`, `padding: 11px`, column flex `gap: 9px`. Contents: 56px-tall photo block (`border-radius: 8px`, `1px solid #3a3d4d`, hatch fill, "PHOTO" label 8px `rgba(233,233,237,.3)` bottom-left); minutes figure (`font-heading` 26px/500, tabular-nums, `#cdf765`, `text-shadow: 0 0 18px rgba(182,242,28,.4)`) + "min" 11px `rgba(233,233,237,.5)`; name 13.5px/500; meta "★ 4.8 · Sindhi biryani" 11.5px `rgba(233,233,237,.42)`, single-line ellipsis. |
| 5 | **Category chips** | Horizontal scroll, `gap: 8px`, `padding: 0 18px 12px`. Chip: 13px/500, `padding: 8px 14px`, `border-radius: 10px`. Inactive `background: rgba(233,233,237,.04)`, `border: 1px solid #2f3242`, colour `rgba(233,233,237,.62)`. Active `background: rgba(145,132,217,.16)`, `border-color: #9184d9`, colour `#c9c2ec`, `box-shadow: 0 0 18px rgba(145,132,217,.28)`. |
| 6 | **Filter row** | `padding: 0 18px 12px`, flex. Left: "Bolt lane only" pill — 11.5px, `padding: 6px 11px`, `border-radius: 99px`, Phosphor `Lightning` 12px. Off: transparent / `1px solid #2f3242` / `rgba(233,233,237,.55)`. On: `rgba(182,242,28,.11)` / `1px solid rgba(182,242,28,.5)` / `#cdf765`, label becomes "Bolt lane only · on". Right: sort button, 11.5px `#9184d9`, Phosphor `Faders` 13px, cycles Fastest → Recommended → Top rated → Cheapest. |
| 7 | **Result count** | `padding: 0 18px 8px`, 10.5px, `letter-spacing:.09em`, uppercase, `rgba(233,233,237,.4)` — e.g. "7 kitchens · sorted by fastest". |
| 8 | **Restaurant list** | `padding: 0 18px 18px`, column flex `gap: 10px`. See **Restaurant row (mobile)**. |
| 9 | **Tab bar** | `position: sticky; bottom: 0`, `margin: 0 14px 26px`, `border-radius: 20px`, `1px solid #2f3242`, `background: rgba(35,37,50,.82)`, `backdrop-filter: blur(16px)`, `box-shadow: 0 10px 30px rgba(0,0,0,.5)`, `padding: 9px 8px`, 5 equal flex items. Each: 21px Phosphor icon + 9.5px/500 label, `gap: 3px`. Active (Home) `#9184d9`; inactive `rgba(233,233,237,.45)`. Items: Home (`House`), Search (`MagnifyingGlass`), Orders (`Bag`), Saved (`Heart`), Profile (`User`). |

#### Restaurant row (mobile)
Flex row, `gap: 12px`, `padding: 11px`, `border-radius: 12px`,
`background: linear-gradient(150deg, rgba(35,37,50,.9), rgba(28,30,40,.7))`, `box-shadow` = shadow-sm.

- **Photo** 76×76, `border-radius: 10px`, `1px solid #3a3d4d`, hatch fill, "PHOTO" 8px label bottom-left.
- **Right column** (flex:1, min-width:0, `gap: 5px`):
  - Title row: name (`font-heading` 15.5px/500, line-height 1.25) + save button (18px Phosphor `Heart`; filled `#9184d9` when saved, outline `rgba(233,233,237,.38)` when not).
  - ETA (`font-heading` 22px/500, line-height 1, tabular-nums, `#cdf765`) — e.g. "20–30 min".
  - Cuisine · distance, 12px `rgba(233,233,237,.45)`.
  - Badge row, `gap: 7px`, each `font-size: 11.5px`, `padding: 3px 7px`, `border-radius: 6px`, `background: rgba(233,233,237,.06)`: ★ rating + review count (`rgba(233,233,237,.35)`); price `$`×N in `#9184d9` with the remainder to 3 in `rgba(233,233,237,.28)`, `letter-spacing:.05em`; optional promo tag on `#2a2647` (accent-900) in `#a99fe1` (accent-300).

### 2. Web — home / discovery (1360px content, 40px gutters)
**Purpose:** same, with filtering promoted to a persistent rail.

`min-height: 100vh`, `background: radial-gradient(80% 42% at 22% 0%, #1e2135 0%, #161826 62%)`, base
type 14px/1.5.

| # | Section | Layout & spec |
|---|---|---|
| 1 | **Sticky nav** | `position: sticky; top: 0; z-index: 20`, `height: 64px`, `background: rgba(22,24,38,.86)`, `backdrop-filter: blur(16px)`, `border-bottom: 1px solid #2f3242`. Inner: `max-width: 1360px`, `padding: 0 40px`, flex, `gap: 28px`. Order: 28px logo mark + "Bolt" (`font-heading` 19px/500); address button (13px, `padding: 7px 11px`, `1px solid #2f3242`, radius 8px, Phosphor `MapPin` 15px `#9184d9`, "Deliver to" in `rgba(233,233,237,.55)` + "12-C Gulberg III" + `CaretDown` 13px; hover `border-color: #9184d9`, `background: rgba(145,132,217,.08)`); search field (flex:1, max 440px, height 38px, `background: rgba(233,233,237,.05)`, `1px solid #2f3242`, radius 8px, `MagnifyingGlass` 16px, 13.5px input, placeholder "Search kitchens or dishes", `:focus` → `border-color: #9184d9`); spacer; Orders and Saved ghost buttons (13px, 16px Phosphor `Bag`/`Heart`, `rgba(233,233,237,.72)`, hover adds `1px solid #2f3242` + full-strength text); Cart outlined button (`1px solid #9184d9`, `#c9c2ec`, radius 8px, `padding: 7px 12px`, count in an 18px `#9184d9` pill with `#161826` text at 11px/600); 34px circular avatar "SA" (`1px solid` accent-700, `rgba(145,132,217,.12)`, `#c9c2ec`, 12px/600). |
| 2 | **Live order tracker** | Full content width, `border: 1px solid #453f6e` (accent-800), radius 8px, `background: linear-gradient(100deg, rgba(145,132,217,.13), rgba(35,37,50,.45) 62%)`, `padding: 14px 18px 16px`, `margin-bottom: 30px`. Top row (flex, wrap, `gap: 12px 18px`): "4′" (`font-heading` 26px/500, tabular-nums, `#cdf765`, `text-shadow: 0 0 22px rgba(182,242,28,.4)`); middle column with stage name 13.5px `#cdf765` + " · Burger Cartel · 2 items" and a 12px `rgba(233,233,237,.42)` sub-line; "Track order" outlined button (`1px solid #9184d9`, `#c9c2ec`, 13px, `padding: 7px 14px`, hover `background: rgba(145,132,217,.12)`). Below: 4-column grid, `gap: 10px`, `margin-top: 16px` — see **Order tracker**. |
| 3 | **Page title** | H1 `font-heading` 34px/500, `letter-spacing: -.02em`, line-height 1.15 — "Fast food, actually fast." Sub-line 14px `rgba(233,233,237,.55)`, `margin-top: 8px`: "12 kitchens open in Gulberg · 5 in the Bolt lane · average 24 min to your door". |
| 4 | **Two-column shell** | `display: grid; grid-template-columns: 222px minmax(0,1fr); gap: 40px; align-items: start`. (`minmax(0,1fr)` matters — without it the inner card grids won't shrink.) |
| 5 | **Left filter rail** | `position: sticky; top: 90px`, column flex `gap: 26px`. Group labels: 10.5px, `letter-spacing:.1em`, uppercase, `rgba(233,233,237,.42)`, `margin-bottom: 10px`. **Categories** — full-width buttons, 13.5px, `padding: 8px 10px`, `border-left: 2px solid` (`#9184d9` active / transparent), `border-radius: 0 6px 6px 0`, count right-aligned 11.5px `rgba(233,233,237,.35)`; active `background: rgba(145,132,217,.12)`, colour `#c9c2ec`; hover `rgba(233,233,237,.05)`. Then a hairline whose ends fade to transparent: `linear-gradient(to right, transparent, #2f3242 12%, #2f3242 88%, transparent)`. **Speed** — "Bolt lane only" full-width toggle, 13px, `padding: 9px 11px`, radius 8px, `Lightning` 14px, state on right (On/Off, 11px `rgba(233,233,237,.4)`); on = `rgba(182,242,28,.1)` / `1px solid rgba(182,242,28,.5)` / `#cdf765` / `box-shadow: 0 0 18px rgba(182,242,28,.18)`; helper text 11.5px `rgba(233,233,237,.4)` "Kitchens that consistently hand off in under 25 minutes." **Price** — three equal buttons `$`/`$$`/`$$$`, 13px, `letter-spacing:.06em`, radius 6px, multi-select, active = `rgba(145,132,217,.14)` / `#9184d9` border / `#c9c2ec`. **Rating** — radio list (Any rating / 4.0 and up / 4.5 and up), 13px, 13px circular dot with 6px inner fill, active `#9184d9`. |
| 6 | **Bolt lane** (hidden once any filter or query is active) | Header: `Lightning` 15px `#b6f21c` with `filter: drop-shadow(0 0 8px rgba(182,242,28,.45))`, "BOLT LANE" `font-heading` 13px/500 `letter-spacing:.1em` uppercase, then "the three quickest kitchens to your door right now" 12.5px `rgba(233,233,237,.42)`; `margin-bottom: 14px`. Grid `repeat(3,1fr)`, `gap: 16px`. Card: flex row `gap: 14px`, `padding: 14px`, radius 12px, `1px solid rgba(182,242,28,.3)`, `background: linear-gradient(150deg, rgba(182,242,28,.09), rgba(30,32,43,.85) 68%)`. 96×96 photo block (radius 8px); minutes figure `font-heading` 32px/500 `#cdf765` + "min" 11.5px; name 15px/500 `margin-top: 10px`; meta 12px `rgba(233,233,237,.42)`. Section `margin-bottom: 38px`. |
| 7 | **Result bar** | Flex baseline space-between, `padding-bottom: 12px`, `border-bottom: 1px solid #2f3242`, `margin-bottom: 20px`. Left: "N kitchens · all categories" `font-heading` 13px/500 `letter-spacing:.1em` uppercase. Right: "Clear filters" text button (12.5px `rgba(233,233,237,.5)`, only when a filter is active) + segmented sort control (`1px solid #2f3242`, radius 8px, 2px padding; options 12.5px, `padding: 5px 11px`, radius 6px). Active option: purple (`rgba(145,132,217,.14)` / `#c9c2ec`) **except "Fastest", which is lime** (`rgba(182,242,28,.1)` / `#cdf765`). Default sort = Fastest. |
| 8 | **Restaurant grid** | `grid-template-columns: repeat(3,1fr)`, `gap: 18px`. See **Restaurant card (web)**. |
| 9 | **Empty state** | `padding: 56px 0`, centred: "Nothing matches that yet." (`font-heading` 17px/500), "Loosen a filter and we'll find you something quick." (13.5px `rgba(233,233,237,.5)`), then a "Clear filters" outlined button. |

#### Restaurant card (web)
Column flex, radius 12px, `background: linear-gradient(160deg, rgba(35,37,50,.85), rgba(28,30,40,.6))`,
`border: 1px solid #3a3d4d`, `overflow: hidden`; hover `border-color: #7a6bc9` (accent-700).

- **Media** 132px tall, hatch fill, `border-bottom: 1px solid #3a3d4d`, "PHOTO" label 8.5px bottom-left.
  - Save button top-right: 30px circle, `1px solid #2f3242`, `background: rgba(22,24,38,.7)`, `backdrop-filter: blur(6px)`, 16px Phosphor `Heart` (filled `#9184d9` when saved, else `rgba(233,233,237,.55)`); hover `border-color: #9184d9`.
  - "BOLT LANE" badge top-left when the kitchen's upper ETA bound ≤ 25: 10px, `letter-spacing:.08em`, `padding: 4px 8px`, `border-radius: 99px`, `background: rgba(22,24,38,.72)`, `backdrop-filter: blur(6px)`, `1px solid rgba(182,242,28,.45)`, `#cdf765`, 10px `Lightning` glyph.
- **Body** `padding: 14px 15px 15px`, column `gap: 7px`, flex:1. Title row: name `font-heading` 16px/500 + ETA `font-heading` 19px/500 tabular-nums `#cdf765`. Cuisine · distance 12.5px `rgba(233,233,237,.45)`. Badge row pinned to the bottom (`margin-top: auto; padding-top: 9px`): rating badge (11px Phosphor `Star` filled `#9184d9`, value + review count), price badge (`$`×N `#9184d9` + remainder `rgba(233,233,237,.28)`), optional promo tag on accent-900/accent-300. All badges 11.5px, `padding: 4px 8px`, radius 6px, `background: rgba(233,233,237,.06)`.

### Order tracker (both platforms)
Four stages, always rendered; index 2 is "current" in the mock.

| Stage | Label | Timestamp |
|---|---|---|
| 0 | Preparing order | 7:41 |
| 1 | Order picked up | 7:52 |
| 2 | Around the corner | now |
| 3 | Delivered | ~8:04 |

Each stage is a column: a 3px `border-radius: 2px` bar, then its glyph and label.

| State | Bar | Glyph | Label colour | Time colour |
|---|---|---|---|---|
| Done (i < current) | `#b6f21c` | Phosphor `Check`, `#b6f21c` | `#e9e9ed` | `rgba(233,233,237,.35)` |
| Current | `#cdf765` + `box-shadow: 0 0 12px rgba(182,242,28,.65)` | filled circle, `#cdf765` | `#e9e9ed` | `#cdf765` |
| Upcoming | `#3a3d4d` (neutral-800) | ring outline, `rgba(233,233,237,.28)` | `rgba(233,233,237,.4)` | `rgba(233,233,237,.35)` |

Web shows the label and timestamp per stage on one 12px row (12px glyph, label ellipsised,
timestamp right-aligned 11px tabular-nums). Mobile is too narrow for four labels: it shows the four
bars with 11px centred glyphs, names the current stage once above them, and bookends with
"Ordered 7:41" / "Delivered ~8:04" below.

Wire this to real order state: stage index, per-stage timestamps, an ETA in minutes for the "4′"
figure, and the kitchen name. The mock is static — no timer.

## Logo
Included as inline SVG in both headers (`viewBox="0 0 120 120"`); 28px in the web nav, 22px in the
mobile brand row. Structure, outermost first:

1. Squircle: `<rect x=4 y=4 width=112 height=112 rx=30 fill="#1b1d2c" stroke="#9184d9">` (stroke 4 at 28px, 5 at 22px).
2. Everything else sits in `<g transform="skewX(-8) translate(8 6)">` — the skew is the forward lean.
3. Three lime draft lines, `stroke-linecap: round`, `opacity: .9`: `M14 44h20`, `M10 56h20`, `M16 68h10`.
4. Two purple wheels: circles at (42,78) and (74,78), `r=11.5`.
5. The bolt, drawn twice — first as a background-coloured halo (`fill` + `stroke: #1b1d2c`, `stroke-linejoin: round`) to knock a gap out of the wheels, then in `#b6f21c`:
   `M68 34L41 66h14l-7 25 30-38H60l8-19z`
6. Helmet, same halo-then-fill trick: circle (68,24) `r=12.5`, halo `#1b1d2c` then `#9184d9`.
7. Visor wedge knocked out of the helmet's front rim, `fill`+`stroke: #1b1d2c`, `stroke-linejoin: round`:
   `M78.6 17.4A12.5 12.5 0 0 1 74.6 34.6L71.2 29.2A6.1 6.1 0 0 0 73.2 20.8Z`

The halo strokes are how the shapes separate without outlines, so they must be painted in that
order and use the **surface** colour behind the mark. When you extract this to an `.svg` asset,
parameterise that colour if the mark will ever sit on a different ground. The wordmark next to it is
live text, not a path: Inter 500, `letter-spacing: .01em`, `#e9e9ed` (19px web / 15px mobile at 600).

Wordmark lockups, the app-icon build and two alternate marks (1a, 1c) are in `Logo.dc.html`.

## Interactions & behaviour
All of it is client-side in the mock; no network calls.

- **Category select** — single-select, "All" is the default and the reset. Filters the list immediately.
- **Search (web)** — controlled input, case-insensitive substring match against name + cuisine + category. Counts as an active filter (hides the Bolt lane, shows "Clear filters").
- **Sort** — web: segmented, click to set. Mobile: one button that cycles the four options. Order: Fastest (default) → Recommended → Top rated → Cheapest. Fastest sorts by the lower ETA bound then the upper; Top rated by rating desc; Cheapest by price tier asc then ETA; Recommended is the authored array order.
- **Bolt lane only** — toggle; keeps kitchens whose **upper** ETA bound ≤ 25.
- **Price** (web) — multi-select over tiers 1–3; no selection means no constraint.
- **Rating** (web) — single-select minimum: 0 / 4.0 / 4.5.
- **Clear filters** — resets category, Bolt toggle, price, rating and query in one action. Appears in the result bar and in the empty state.
- **Save (heart)** — per-restaurant toggle; the nav's "Saved" count follows it. Seeded on: Kolachi Biryani House, Zamzama Shawarma.
- **Bolt lane visibility** (web) — shown only when no filter and no query are active; it's a browse device, not a result set.
- **Empty state** — replaces the grid when the filter set matches nothing.
- **Hover** — cards lift their border to accent-700; ghost nav buttons gain a divider border; outlined buttons gain a `rgba(145,132,217,.12)` wash. Every interactive element needs a hover tint.
- **Focus** — `:focus-visible { outline: 2px solid #9184d9; outline-offset: 2px }` globally. Never leave the browser default.
- **Not built, needs product decisions:** address picker, cart, profile, tab-bar destinations, restaurant detail page, real order tracking (the tracker is a static stage index), pagination/infinite scroll, skeleton and error states, and any auth.

### Responsive
The mock is authored at two fixed sizes and does **not** include the in-between. You'll need to define:
- **Web ≥1440px** — content is capped at 1360px and centres; nothing stretches.
- **Web ~1024–1280px** — restaurant grid to 2 columns; Bolt lane to 2 columns or a horizontal scroller.
- **Web <1024px** — collapse the left rail into a filter drawer or a chip row (the mobile pattern), stack the nav's search below the brand row.
- **Mobile** — 402px reference; everything is fluid except the fixed photo blocks and the 150px lane cards. Keep hit targets ≥44px (the 40px header buttons are the floor; pad their tap area).

## State management
Web (`Home Screen - Web.dc.html`):

```
cat: string        // 'All' | category name
sort: number       // index into SORTS
query: string
boltOnly: boolean
prices: Record<1|2|3, boolean>
minRating: number  // 0 | 4 | 4.5
favs: Record<restaurantId, boolean>
```

Mobile is the same minus `query`, `prices` and `minRating` (its filter row carries only the Bolt
toggle and sort). Derived, not stored: the filtered+sorted list, the result count string, the Bolt
lane (three fastest, computed from the full set — never from the filtered set), `hasFilters`, and
the saved count.

Data fetching for a real build: restaurants for the delivery address (with cuisine, rating, review
count, ETA bounds, price tier, distance, promo tag, image), the active order's stage and ETA, and
the customer's saved list. Filtering and sorting are cheap enough to keep client-side over a
neighbourhood-sized result set; if the catalogue grows, move sort and filter to the query.

### Restaurant shape
```
{ id, name, cat, cuisine, rating: number, reviews: string,
  mins: '20–30', price: 1|2|3, dist: '1.4 km', tag?: string }
```
`mins` is a display string parsed for sorting — in a real API prefer `etaMin`/`etaMax` integers and
format at the edge. `reviews` is pre-abbreviated ("3.4k") in the mock; format from a real count.
Categories: All, Biryani, Pasta, Pizza, Fast Food, Desi, Pan Asian, Desserts.

## Design tokens

### Colour
| Token | Hex | Use |
|---|---|---|
| bg | `#161826` | page ground |
| bg gradient (web) | `radial-gradient(80% 42% at 22% 0%, #1e2135 0%, #161826 62%)` | page |
| bg gradient (mobile) | `radial-gradient(120% 55% at 50% 0%, #20233a 0%, #161826 56%)` | page |
| surface | `#232532` | raised surfaces |
| surface (icon plate) | `#1b1d2c` | logo squircle |
| text | `#e9e9ed` | primary text |
| text muted | `rgba(233,233,237,.55)` | secondary |
| text faint | `rgba(233,233,237,.42)` / `.35` / `.28` | meta, counts, disabled marks |
| divider | `#2f3242` | 1px borders |
| neutral-800 | `#3a3d4d` | photo-block borders, inactive bars |
| neutral-700 | `#4a4e60` | radio outlines |
| accent (purple) | `#9184d9` | brand, chrome, ratings, focus |
| accent-200 | `#c9c2ec` | text/icons on purple tints |
| accent-300 | `#a99fe1` | small text on purple tints |
| accent-700 | `#7a6bc9` | hover borders |
| accent-800 | `#453f6e` | tinted borders |
| accent-900 | `#2a2647` | tinted fills |
| accent-2 (lime) | `#b6f21c` | speed: bolt, lightning, done bars |
| accent-2 text | `#cdf765` | ETAs, minute figures, current stage |
| purple tints | `rgba(145,132,217,.08 / .12 / .14 / .16)` | hovers, active chips |
| lime tints | `rgba(182,242,28,.09 / .1 / .11 / .3 / .45 / .5)` | lane cards, toggles, borders |
| glass | `rgba(22,24,38,.7–.86)` + `backdrop-filter: blur(6–16px)` | nav, tab bar, badges |

Contrast note: the accent-on-ground pair clears 3:1, which covers icons, large type and chrome but
**not** body copy. For paragraph-size purple text use `#a99fe1` (accent-300) or lighter. Lime at
`#cdf765` is safe for the small labels it's used on.

### Type
Inter throughout (`--font-heading` and `--font-body` are both Inter). Weights 400/500/600 only —
never bolder than 500 for headings.

| Role | Size / weight |
|---|---|
| H1 (web) | 34px / 500, `letter-spacing: -.02em`, line-height 1.15 |
| Section label | 13px / 500, `letter-spacing: .1em`, uppercase |
| Card title (web) | 16px / 500 |
| Card title (mobile) | 15.5px / 500, line-height 1.25 |
| Big minutes | 32px (web lane) / 26px (mobile lane) / 22px (mobile row) / 19px (web card) / 500, tabular-nums |
| Body | 14px / 400 (web), 13px (mobile) |
| Meta | 12–12.5px / 400 |
| Badge | 11.5px / 400 |
| Micro label | 10–10.5px, `letter-spacing: .08–.1em`, uppercase |

Every number that changes (ETAs, counts, prices, timestamps) uses
`font-variant-numeric: tabular-nums`.

### Spacing, radius, elevation
Nocturne's scale is compact (0.7× density). Values in use: 2, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 16,
18, 20, 26, 28, 30, 38, 40, 56, 64 px. Page gutters 40px (web) / 18px (mobile); grid gaps 16–18px;
rail group gap 26px.

Radii: `--radius-sm` 6px, `--radius-md` 8px, `--radius-lg` 12px; 20px for the mobile tab bar, 30px
for the logo squircle, `99px` for pills and circles.

Shadows: `--shadow-sm` on cards; the tab bar uses `0 10px 30px rgba(0,0,0,.5)`. Glows are
`0 0 12–22px` of the accent at 18–65% alpha. Don't stack shadows — on this ground elevation is an
edge plus ambient darkness.

## Assets
- **Icons — Phosphor** (https://phosphoricons.com), inlined as 256-viewBox SVG paths in the mocks. Regular weight outline for most; `Star` and the saved `Heart` use the **fill** variant. Full list: User, MagnifyingGlass, Heart (regular + fill), Star (fill), Lightning (fill), Faders, Bag, CaretDown, MapPin, House, Check. Install the real package rather than lifting the paths.
- **Logo** — inline SVG, spec above; no external file. Export to `.svg` (mark, wordmark lockup, app icon) as part of the build.
- **Photography** — none. Every image is a hatched placeholder:
  `repeating-linear-gradient(135deg, #262939 0 6px, #1e2029 6px 12px)` (125deg and 8px/16px on the web card media) with a 1px `#3a3d4d` border and a "PHOTO" caption. Replace with real imagery at the same box sizes: 76×76 and 96×96 (rows/lane), 132px-tall full-width (web card media), 56px-tall (mobile lane).
- **Fonts** — Inter, weights 400–600.

## Files
In this bundle:

| File | What it is |
|---|---|
| `Home Screen - Web.dc.html` | **Web home/discovery — the primary desktop reference.** |
| `Home Screen.dc.html` | **Mobile.** Contains two turns of exploration as stacked sections. Build from the **top** section, id `2a` ("Bolt") — that's the approved design. The section below it (`1a`/`1b`/`1c`) is superseded exploration under the earlier name "Tiffin", kept for context; ignore it. |
| `Logo.dc.html` | Three logo directions. **`1b` is approved** (the squircle app-icon build now in both headers). `1a` and `1c` are alternates. |
| `Existing Prototype (recreation).dc.html` | A faithful recreation of the repo's current `index.html` (menu, cart, simulated order tracking) on its original light palette. Reference for what exists today — **not** part of the new design. |
| `ios-frame.jsx` | The iPhone bezel/status-bar wrapper used to present the mobile screens. Presentation scaffolding only — do not port it. |
| `_ds/nocturne-*/styles.css` | The Nocturne token sheet and component layer. The clean source for the token values above; port the `:root` custom properties to your app. |
| `_ds/nocturne-*/readme.md` | Nocturne's own usage guide (direction, colour, type, do/don't). |

How to read a `.dc.html`: the template markup is the top block, the logic class (`renderVals()`
returns everything the template interpolates) is in the `<script data-dc-script>` at the bottom.
Styling is entirely inline in the template — that's a constraint of the design tool, not a
recommendation. `<sc-for list=… as=…>` is a repeat and `<sc-if value=…>` a conditional; both become
ordinary `.map()` / conditional rendering in your framework.

To view a design as intended, open the file in a browser — they're self-contained apart from the
`_ds/` stylesheet and `support.js` runtime.

## Working in the repo (`shahzaibq12/food-delivery-mvp`, branch `dev`)
The repo currently holds a single static `index.html` prototype — the light-palette menu/cart/
tracking demo recreated in this bundle. This design replaces that screen entirely: new brand
(Bolt), new dark palette, and a restaurant-discovery model rather than a single-kitchen menu. The
existing cart and order-tracking logic is the one piece worth carrying forward conceptually; its
stage machine maps onto the four-stage tracker.

Suggested sequence:

1. Branch off `dev` (e.g. `feat/bolt-home`).
2. Scaffold the framework and commit the token layer first (Nocturne's `:root` variables, Inter, Phosphor, the global `:focus-visible` rule) — everything downstream reads from it.
3. Extract the logo to `.svg` assets (mark, lockup, app icon).
4. Build the shared pieces: restaurant card, ETA figure, badge, category control, order tracker.
5. Compose the web screen, then the mobile screen, then fill in the responsive middle.
6. Wire real data behind the shape documented above; keep the dummy set as fixtures for tests.
7. Open a PR into `dev` with screenshots at 1440px and 402px next to these references.

Do not commit anything from this bundle into the app source — `.dc.html` files, `ios-frame.jsx` and
`support.js` are design-tool artefacts. Keep the bundle as reference material (or in a `design/`
folder outside the build) and port only the token values and SVG paths.
