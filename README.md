# Zenin Market Web

> Frontend for **Zenin Market — Fine Foods & Provisions**, a fictional supermarket.
> A touch-friendly deli scale screen, a back office and a queue display.

![Status](https://img.shields.io/badge/status-Phase%200%20(setup)-orange)
![Angular](https://img.shields.io/badge/Angular-standalone%20%2B%20signals-DD0031?logo=angular&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6?logo=typescript&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

## What is this?

Zenin Market is a portfolio project that models how a real supermarket **deli counter** works.
This repository is the **Angular app**. The backend lives in
[`zenin-market-api`](https://github.com/Leonix64/zenin-market-api).

> ⚠️ Everything here is fictional: names, brands, prices, logos and addresses.

## Screens

### Scale (clerk)
- Category grid and product grid with big touch buttons
- PLU keypad: type the code, press Enter, the product loads
- Text search (`contains` and `starts with`)
- Detail panel: price, simulated weight, tare buttons (8 / 16 / 32 oz), total
- Sell-by dialog: days, resulting date, print date / time
- Print button and recent labels list with reprint

### Office (admin)
- Login
- Products list and form
- Category list and grid layout
- Specials list / calendar

### Queue (later)
- Clerk controls: next, repeat and cancel number
- Customer ticket with number, time and estimated wait
- Live display screen

📸 Screenshots will be added in Phase 5.

## Tech stack

| Area | Choice |
|---|---|
| Framework | Angular (standalone components) |
| State | Signals (no NgRx) |
| Routing | Lazy-loaded feature routes |
| Language | TypeScript |
| API contract | Types generated from the API's OpenAPI spec |
| Design | Touch-first, built for a full-screen tablet-like display |

## Project structure (planned)

```
src/app/
  core/       auth, http interceptors, guards, config
  shared/     ui components, pipes (money, weight), utils
  features/
    scale/    category grid, product grid, detail, keypad, search, sell-by
    office/   products, categories, specials
    queue/
    auth/     login
  app.routes.ts
```

## Offline-first rules

Offline mode is built last, but these rules apply from day one:

1. Every label gets a **client-generated UUID**.
2. The scale screen reads products from a **local cache**, not straight from the network on every tap.
3. Printing **saves the label locally first**, then syncs it.

## Getting started

🚧 Setup instructions will be added during Phase 0 (`chore/frontend-setup`).

## Roadmap

- [ ] **Phase 0** — Setup: Angular project, linting, environment config
- [ ] **Phase 1** — Scale core screens
- [ ] **Phase 2** — Office screens and login
- [ ] **Phase 3** — Queue screens with live updates
- [ ] **Phase 4** — Offline mode
- [ ] **Phase 5** — Polish: tests, screenshots, deploy, demo video

## License

[MIT](LICENSE)
