# SEO vs GEO Demo — Project Guide

## What is this?
An interactive educational page comparing **SEO** (Search Engine Optimization) vs **GEO** (Generative Engine Optimization) on the same topic ("Škoda Kodiaq"). Two side-by-side scrollable panels with numbered hotspots that explain the differences.

**Live URL:** https://seo-vs-geo-demo.netlify.app

## Project structure
```
seo-vs-geo-demo/
├── index.html          ← Single-file app (HTML + CSS + JS, no build step)
├── CLAUDE.md           ← This file
├── .netlify/           ← Netlify link config (auto-generated)
└── netlify.toml        ← Deploy config
```

## Tech stack
- **Pure HTML/CSS/JS** — no framework, no dependencies, no build tools
- **Font:** Inter (Google Fonts CDN)
- **Design:** Škoda Auto-inspired — white background, forest green (#31694B), mint (#78FAAE), pill buttons, bold/light font contrast
- **Hosting:** Netlify (site name: `seo-vs-geo-demo`)

## Design system
| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#FFFFFF` | Main background |
| `--bg-alt` | `#F4F6F5` | GEO panel background |
| `--green-dark` | `#31694B` | GEO headings, badges, accents |
| `--green-deep` | `#0E3A2F` | Code blocks background |
| `--mint` | `#78FAAE` | SEO badges, CTA, pill buttons |
| `--text` | `#161718` | Primary text |
| `--text-sec` | `#464748` | Body text (weight 300) |
| `--text-ter` | `#7C7D7E` | Captions, labels |
| `--border` | `#E4E4E4` | Borders, dividers |
| Font weight headings | 700 | All headings |
| Font weight body | 300 | All body text |

## Key features
1. **Split layout** — two independently scrollable panels (SEO left, GEO right)
2. **Hotspots** — numbered circles on text, hover shows tooltip
3. **Click-to-spotlight** — clicking a hotspot darkens the page (overlay), keeps hotspot + tooltip visible
4. **Tooltip data** — all in JS `tooltips` object, each with `type`, `title`, `body`, `vs` fields
5. **Hero banners** — inline SVG car illustrations with different captions (SEO: alt text, GEO: source citation)

## How to edit content

### Article text
Search for `panel-seo` or `panel-geo` in HTML. Content is standard HTML (h1, h2, p, table, ul, blockquote).

### Hotspots
Each hotspot is a `<span class="hotspot" data-tooltip="KEY">text</span>` followed by `<span class="hotspot-num" data-tooltip="KEY">N</span>`. The KEY maps to the `tooltips` JS object.

### Tooltip explanations
In the `<script>` section, find `const tooltips = { ... }`. Each entry:
```js
'seo-h1': {
    type: 'seo',          // 'seo' or 'geo'
    title: 'Short title',
    body: 'Explanation with <strong>HTML</strong>',
    vs: 'What the other side does differently'
}
```

### Adding a new hotspot
1. Wrap text: `<span class="hotspot" data-tooltip="my-key">text</span><span class="hotspot-num" data-tooltip="my-key">N</span>`
2. Add entry to `tooltips` object in JS
3. Increment hotspot numbers

## How to deploy

### First-time setup (on a new machine)
```bash
npm install -g netlify-cli
netlify login          # Opens browser for auth
cd /path/to/seo-vs-geo-demo
netlify link --name seo-vs-geo-demo
```

### Deploy changes
```bash
cd /path/to/seo-vs-geo-demo
netlify deploy --dir=. --prod
```

The site deploys to the same URL every time: https://seo-vs-geo-demo.netlify.app

## Language
Content is currently in **English**. Tooltip labels use "SEO Principle" / "GEO Principle" and "In the GEO/SEO version".

## Notes
- All content is in a single `index.html` file (~60KB)
- No favicon is set intentionally
- Mobile: panels stack vertically below 600px
- The overlay spotlight uses CSS `position: fixed` with SVG mask — no external libraries
