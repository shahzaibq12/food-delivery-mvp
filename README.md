# Kettle & Crumb — food delivery MVP

A single-page food delivery prototype. One `index.html`, no build step, no dependencies.

## Run it

Open `index.html` in a browser. That's it.

For a local server (optional):

```bash
python -m http.server 8000
```

## What it does

- **Menu** — six fixed items with emoji placeholders and dummy prices.
- **Cart** — add/remove items, quantity per line, subtotal plus a flat $2.50 delivery fee.
- **Place order** — creates an order with a generated `KC-####` id.
- **Tracking** — each order advances through Confirmed → Preparing → On the way → Delivered on a simulated timeline (36s end to end), with a live countdown.
- **Persistence** — orders are kept in `localStorage`, so tracking survives a page reload. "Clear demo data" wipes them.

Order state is derived from the order's `placedAt` timestamp rather than a running timer, so progress stays correct across reloads.

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

- CSS custom properties at the top define the palette; light and dark themes both defined.
- `MENU` and `STAGES` constants near the top of the script — edit these to change the catalogue or the tracking timeline.
- Three render functions: menu (once), `renderCart()`, `renderOrders()` (re-run every second).

## Not included

No backend, no auth, no payment, no real restaurants or couriers. Prices and delivery times are made up.
