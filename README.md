# Bolt — food delivery MVP

A single-page food delivery prototype for Lahore whose one differentiator is **speed**. One
`index.html`, no build step, no dependencies.

## Run it

Open `index.html` in a browser. That's it.

For a local server (optional):

```bash
python -m http.server 8000
```

## What it does

The home / discovery screen a signed-in customer lands on, in two forms driven off one state
object — desktop at and above 1024px, mobile below it.

- **Discovery** — twelve kitchens with cuisine, rating, review count, ETA range, price tier and distance.
- **Bolt lane** — the three fastest kitchens, always computed from the whole catalogue rather than
  the filtered set. Hidden on desktop as soon as any filter or query is active; it's a browse
  device, not a result set.
- **Filtering** — category (single-select), "Bolt lane only" (upper ETA bound ≤ 25 min), price tier
  (multi-select) and minimum rating. Desktop puts these in a persistent left rail; mobile carries
  the category chips and the Bolt toggle. "Clear filters" resets all of them plus the query.
- **Search** (desktop) — case-insensitive substring match over name, cuisine and category.
- **Sort** — Fastest (default), Recommended, Top rated, Cheapest. Desktop uses a segmented control;
  mobile cycles one button.
- **Save** — per-kitchen heart; the nav's "Saved" count follows it.
- **Live order tracker** — four stages (Preparing → Picked up → Around the corner → Delivered) with
  the ETA as the loudest figure on the screen.

The tracker reads a static stage index from the `ORDER` object — wire it to real order state.
Nothing here talks to a network; `RESTAURANTS` and `ORDER` are fixtures.

## Design

Implemented from the Bolt handoff in `design/bolt-home/` (the `.dc.html` files there are design
references, not app source). Two accents with non-interchangeable jobs: purple `#9184d9` is brand
and chrome, electric lime `#b6f21c` is speed and time only — every ETA, the Bolt lane, the tracker.
Tokens live as CSS custom properties in `:root`; icons are Phosphor paths inlined as SVG, and the
logo is inline SVG.

Photography is a hatched placeholder at the final box sizes (76×76 and 96×96, 132px-tall card
media, 56px-tall lane cards) — swap in real imagery at those sizes.

## Branching

```
feature/<name>  ->  dev  ->  prod
```

- **`prod`** — released state. Only ever updated by merging `dev`. This is the branch that gets published.
- **`dev`** — integration branch and the repo default, so pull requests target it unless you say otherwise. Features land here first.
- **`feature/<name>`** — one per change, branched from `dev`, merged back via pull request.

Starting a feature:

```bash
git checkout dev && git pull
git checkout -b feature/my-change
```

Releasing: open a pull request from `dev` into `prod`.

## Structure

Everything lives in `index.html`:

- CSS custom properties at the top of the stylesheet define the palette, radii and shadow. Dark
  ground only — the design is single-theme by intent.
- `CATS`, `SORTS`, `RESTAURANTS` and `ORDER` constants near the top of the script — edit these to
  change the categories, the sort options, the catalogue or the in-flight order.
  - Adding a category: add it to `CATS` (array order is rail and chip order), then tag kitchens
    with it via their `cat` field. The per-category counts are derived.
  - Restaurant shape: `{ id, name, cat, cuisine, rating, reviews, mins: '20–30', price: 1|2|3,
    dist, tag? }`. `mins` is a display string parsed for sorting; a real API should send
    `etaMin`/`etaMax` integers and format at the edge.
- One `state` object, one `render()`. `visible()` derives the filtered and sorted list; `boltLane()`
  derives the three fastest. Nothing derived is stored.
- `webView()` and `mobView()` both render on every pass; CSS decides which is shown. Clicks are
  handled by one delegated listener keyed on `data-act`.
- Controls not yet wired carry `data-act="noop"` — see **Not included**.

## Not included

No backend, no auth, no payment, no real restaurants or couriers. Prices and delivery times are made up.

These need product decisions before they can be built, and are inert in the UI today: the address
picker, cart, profile, tab-bar destinations, the restaurant detail page, real order tracking (the
tracker is a static stage index), pagination, and skeleton and error states.
