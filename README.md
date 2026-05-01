# Dataline Website

Marketing site for **Dataline** — `dataline.xyz`.

Static HTML deployed on Vercel. No build step. Each page is a single self-contained `.html` file with inline CSS and JS.

## Routes

| Route | File |
|---|---|
| `/` | `index.html` — homepage |
| `/flowagent` | `flowagent.html` |
| `/ghostdriver` | `ghostdriver.html` |
| `/chatpilot` | `chatpilot.html` |
| `/data` | `data.html` — flagship product |
| `/api` | `api.html` — API reference |
| `/mcp` | `mcp.html` — MCP server install |
| `/pricing` | `pricing.html` |
| `/waitlist` | `waitlist.html` — FormSubmit-backed signup |
| `/thanks` | `thanks.html` — post-signup confirmation |
| `/blog` | `blog.html` |
| `/blog-flowagent`, `/blog-ghostdriver`, `/blog-chatpilot-2-5m`, `/blog-data-layer`, `/blog-full-chain-ai-stack` | individual posts |
| `/logos` | `logos.html` — brand mark exploration |

`vercel.json` enables `cleanUrls: true` so `.html` is stripped.

## Brand assets

- `favicon.svg` / `favicon.ico` / `favicon-32.png` / `favicon-512.png` / `apple-touch-icon.png`
- `og-image.png` / `og-image.svg` (1200×630)
- `site.webmanifest`

`BRANDING.md` has typography, palette, and component spec.

## Deploy

Connect this repo to a Vercel project. Domain: `dataline.xyz` (primary) with `tearline.io` set to redirect once DNS is cut over.
