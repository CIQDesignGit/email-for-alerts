# CommerceIQ Daily Update — HTML Email

Ready-to-preview HTML email for **Sales Agent** daily updates. Styling uses **Tailwind CSS v4** and **@ciq-dev/ciq-design-system** CSS variables / tokens (`--brand`, `--fg-brand`, `--action-primary`, …).

## Quick start

```bash
npm install
npm run preview   # builds CSS, then opens emails/daily-update.html
```

Rebuild while editing:

```bash
npm run watch
```

## Design system + Tailwind

| Layer | Path |
|---|---|
| DS tokens + `@theme` | `tokens/ciq-email-tokens.css` |
| Email layout / components | `styles/email.css` |
| Built stylesheet | `emails/email.css` |
| Template | `emails/daily-update.html` |

In **web apps**, use the package directly:

```js
import "@ciq-dev/ciq-design-system/styles";
import { Button, Badge } from "@ciq-dev/ciq-design-system";

<Button variant="default">View all issues</Button>
<Badge variant="defaultLight">Lost buy box</Badge>
```

This email repo mirrors the same tokens:

- **CSS variables** — `--fg-brand`, `--action-primary`, `--border-default`, `--feedback-danger`, …
- **Tailwind utilities** — `bg-canvas`, `text-fg-primary`, `font-sans`, …
- **Component classes** — `.email-cta` = Button `default`; `.email-badge` = Badge `defaultLight`

## What’s in the email

| Section | Purpose |
|---|---|
| Header | CommerceIQ · Daily Update · Sales Agent |
| Summary metrics | Open issues (+ new SKUs) · Cumulative OPS at risk |
| Breakdowns | By issue type · By category (SKU counts) |
| Top 5 impacted SKUs | Product · Issues (chips) · Projected EOW gap to plan |
| CTA | “View all issues” (DS `action-primary`) |
| Footer | Ownership note · address · preference / unsubscribe |

## Before you send to clients

Most ESPs strip external stylesheets and do not support CSS variables. For production sends:

1. Inline / bake styles for the ESP (or host a self-contained build)
2. Replace the CTA link with your real URL
3. Host product images on a CDN and update `src` URLs
4. Replace sample numbers / SKUs with live API data
5. Update preference / unsubscribe links in the footer

## Deploy on Vercel

This project is a static site — Vercel serves the `emails/` folder after `npm run build`.

- **Output directory:** `emails` (configured in `vercel.json`)
- **Root URL:** rewrites to `daily-update.html`
- Push to `main` to redeploy

```bash
npm run build   # compiles CSS + copies index.html into emails/
```
