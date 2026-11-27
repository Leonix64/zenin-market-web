# Zenin Market Web

> Frontend for **Zenin Market — Fine Foods & Provisions**, a fictional supermarket.
> A touch-friendly deli scale screen, a back office and a queue display.

![Status](<https://img.shields.io/badge/status-Phase%200%20(setup)-orange>)
![Angular](https://img.shields.io/badge/Angular-standalone%20%2B%20signals-DD0031?logo=angular&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6?logo=typescript&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

## What is this?

Zenin Market is a portfolio project that models how a real supermarket **deli counter** works:
a touch-screen scale where the clerk picks a product, weighs it and prints a label, plus a back
office where products, categories, prices and specials are managed.

This repository is the **Angular app**. The backend lives in
[`zenin-market-api`](https://github.com/Leonix64/zenin-market-api).

> ⚠️ Everything here is fictional: names, brands, prices, logos and addresses.

## Screens

### Scale (clerk, no login screen)

- Category grid (5×3) and product grid with pages (15 slots per page, ▲ / ▼ PAGE buttons)
- PLU keypad: type the code, press Enter, the product loads
- Text search (`contains` and `starts with`)
- Detail panel: active price, simulated weight, tare buttons (8 / 16 / 32 oz) for weight items,
  quantity − / + for piece items, live total
- SPECIAL banner when the active price comes from a special
- Sell-by dialog: number of days or exact date, print date and print time
- PRINT sends the label directly. A total over $99.99 blocks printing.
- Recent labels list (read-only)
- Demo helpers: weight simulator and a simulated printer panel that shows the printed label
- One-time station setup (`/setup`)

### Office

- Login (email and password)
- Products list and form
- Categories list and 5×3 grid layout
- Product grid per category, with pages
- Specials list and form, with overlap check
- "Open scale" link in the sidebar

### Queue (Phase 3, behind the `queueEnabled` flag)

- Clerk controls: next, repeat and cancel number
- Customer ticket with number and time
- Live display screen

📸 Screenshots will be added in Phase 5.

## Routes

| Route     | Who           | What                                                                             |
| --------- | ------------- | -------------------------------------------------------------------------------- |
| `/`       | Scale station | Scale screens. No login: the session comes from the station's long-lived cookie. |
| `/setup`  | Office user   | One-time link between a device and a scale station.                              |
| `/office` | Office role   | Login and back office.                                                           |

## Tech stack

| Area         | Choice                                                                            |
| ------------ | --------------------------------------------------------------------------------- |
| Framework    | Angular 22 (standalone components)                                                |
| State        | Signals (no NgRx)                                                                 |
| Routing      | Lazy-loaded feature routes                                                        |
| Language     | TypeScript (strict)                                                               |
| Styles       | SCSS, one `.scss` per component, shared tokens in `src/styles/` (no Tailwind)     |
| UI helpers   | `@angular/cdk` (dialogs, overlays, drag and drop)                                 |
| Barcode      | `jsbarcode` draws the digits that the API computes                                |
| i18n         | English only for now, ready for Spanish (Transloco)                               |
| API contract | Types generated from the API's OpenAPI spec                                       |
| Design       | Touch-first. Scale screens are designed at 800×480 and scaled to fit the display. |

## Project structure (planned)

```
src/
  app/
    core/       auth, http interceptors, guards, config
    shared/     ui components, pipes (money, weight, dates), utils
    features/
      scale/    category grid, product grid, detail, keypad, search, sell-by, recent labels, setup
      office/   products, categories, product grid, specials
      queue/
      auth/     login
    app.routes.ts
  styles/       tokens, mixins, global reset
```

Folders are created only when a file lives in them.

## Offline-first rules

Offline mode is built last, but these rules apply from day one:

1. Every label gets a **client-generated UUID** (`crypto.randomUUID()`).
2. The scale screen reads products from a **local cache**, not straight from the network on every tap.
3. Printing **saves the label locally first**, then syncs it.

## Getting started

### Requirements

- Node.js 24 (see `.node-version`)
- npm 11
- Angular CLI 22.3 (optional, `npx ng` works too)

### Run it

```bash
npm ci
npm start
```

Open <http://localhost:4200>. The app is still an empty shell until Phase 1.

### Scripts

| Command         | What it does                  |
| --------------- | ----------------------------- |
| `npm start`     | Dev server with live reload   |
| `npm run build` | Production build into `dist/` |
| `npm test`      | Unit tests                    |

Lint and format scripts will be added in the tooling PR.

### Backend

The app needs [`zenin-market-api`](https://github.com/Leonix64/zenin-market-api) running locally
from Phase 1 on. Setup steps for the proxy will be added when the API is ready.

## Roadmap

- [ ] **Phase 0** — Setup: Angular project, linting, CI, styles foundation, routes skeleton
- [ ] **Phase 1** — Scale core screens
- [ ] **Phase 2** — Office screens, login and station setup
- [ ] **Phase 3** — Queue screens with live updates
- [ ] **Phase 4** — Offline mode
- [ ] **Phase 5** — Polish: tests, screenshots, deploy, demo video

## License

[MIT](LICENSE)
