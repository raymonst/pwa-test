# Orbit Wallet PWA - Project Memory

## Project Overview
- **Name:** Orbit Wallet (brand: Orbit)
- **Type:** Progressive Web App (PWA) — fintech demo wallet
- **Deployment:** GitHub Pages
- **Architecture:** Single-file SPA, vanilla JS, no frameworks

## Key Files
- `index.html` — Entire app (~4190 lines): HTML + CSS + JS
- `sw.js` — Service worker, cache-first strategy, cache name `orbit-wallet-v3`
- `manifest.json` — PWA manifest, start URL `/wla-pwa-test/`, theme `#001b96`
- `icons/` — 192x192 and 512x512 maskable PNGs
- `bg-transaction-details.png` — Background for transaction detail page

## App Structure (Pages/Tabs)
**Bottom nav tabs (cross-fade transition):**
- Wallet (home) — balance, transactions, banners
- Payment — money transfer entry
- Card — credit card with 3D flip
- Perks — rewards/cashback

**Drill-down pages (slide-in from right):**
- Transfer Money — numpad amount input, account selection
- Review Transfer — confirmation screen
- Transaction Detail — detailed view with background image
- Placeholder pages (Receive, Savings, Payees, Shell Offer)

## JavaScript Modules (IIFE Pattern)
Window-exported public APIs: `switchTab`, `tfReset`, `openTxDetail`, `switchAccount`, `navigateTo`, `navigateBack`, `setFilter`, `openTxDetail`, `closeTxDetail`, `toggleCardDetails`

Key modules:
- **Page Navigation** — `navigateTo/navigateBack`, `switchTab`, history.pushState, popstate handlers
- **Transfer Money** — numpad, font-scaling amount display, bottom sheet account selector, edge swipe gesture
- **Review Transfer** — confirmation with back/edit/submit
- **Account Switcher** — panel slide + swipe gesture (0=checking, 1=savings), `MAX=1890.27`
- **Card Flip** — 3D CSS rotateY, toggles on button click
- **Transaction Detail** — `openTxDetail(data)` populates modal from tx object
- **Filter Pills** — `setFilter(btn, filter)` shows/hides transactions by `data-type` (in/out/all)

## Navigation System
- Tab switching: CSS opacity cross-fade, z-index swap
- Drill-down: slide push right (`translateX`), 0.32s cubic-bezier
- Back/pop: slide out left, history API
- Account panels: swipe gesture (25% threshold to snap)
- Bottom sheet: translateY from 100% to 0
- History API: `pushState` on navigation, `popstate` to sync UI

## CSS Design System
- 80+ CSS variables in `:root` for colors, spacing, typography
- Brand color: `#001b96` (dark blue)
- Fonts: Figtree (body), Cabin (logo/headlines)
- Mobile-first, 500px max-width
- PWA safe areas: `env(safe-area-inset-*)` on top bar and nav

## Known Issues / History
- Nav dot fix attempts introduced additional bugs — reverted multiple times (see git log)
- Branch `claude/pensive-herschel` is a worktree for active dev

## Data
- No real API calls — all hardcoded demo data in HTML
- No localStorage persistence
- Transfer max: `MAX = 1890.27` (checking balance)
- TO_ACCOUNTS: savings (internal) and Chase Checking ••6789 (external)
