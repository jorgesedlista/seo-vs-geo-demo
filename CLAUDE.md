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

### Workflow (two contributors)
We share this repo on GitHub. Each contributor has their **own Netlify site** (free tier) for previewing changes. The production URL is managed by Jirka.

- **Production:** https://seo-vs-geo-demo.netlify.app (Jirka deploys)
- **Your preview:** your own Netlify URL (you create & deploy)

### First-time setup (collaborator)
```bash
# 1. Clone the repo
git clone https://github.com/jorgesedlista/seo-vs-geo-demo.git
cd seo-vs-geo-demo

# 2. Install Netlify CLI
npm install -g netlify-cli

# 3. Login to YOUR OWN Netlify account (free)
netlify login

# 4. Create your own site for preview
netlify init
#   → "Create & configure a new site"
#   → Pick your team
#   → Choose a site name (e.g. "seo-geo-preview-katka")
#   → Build command: leave empty (just press Enter)
#   → Publish directory: .

# 5. Deploy to your preview URL
netlify deploy --dir=. --prod
```

Your preview site will be at something like `seo-geo-preview-katka.netlify.app`.

### Daily workflow
```bash
# 1. Pull latest changes
git pull

# 2. Edit with Claude
claude

# 3. Preview your changes
netlify deploy --dir=. --prod
# → deploys to YOUR preview URL

# 4. Push changes to shared repo
git add -A
git commit -m "description of changes"
git push
```

Jirka will pull your changes and deploy to the production URL when ready.

### Production deploy (Jirka only)
```bash
git pull
netlify deploy --dir=. --prod
# → deploys to https://seo-vs-geo-demo.netlify.app
```

## Language
Content is currently in **English**. Tooltip labels use "SEO Principle" / "GEO Principle" and "In the GEO/SEO version".

## Notes
- All content is in a single `index.html` file (~60KB)
- No favicon is set intentionally
- Mobile: panels stack vertically below 600px
- The overlay spotlight uses CSS `position: fixed` with SVG mask — no external libraries
