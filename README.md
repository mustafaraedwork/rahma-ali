# Viktor and Paula — Wedding Invitation

A clean, locally-hosted version of the original Tilda page (`webgency.tilda.ws/template5`).
Same design, same behavior — just organized into a normal project layout with relative paths.

## Project layout

```
viktor-and-paula/
├── index.html                       Main page (was template5.html)
├── README.md
└── assets/
    ├── css/
    │   ├── tilda-grid-3.0.min.css
    │   ├── tilda-animation-2.0.min.css
    │   ├── tilda-popup-1.1.min.css
    │   ├── tilda-forms-1.0.min.css
    │   ├── page.min.css             Per-page styles (was tilda-blocks-page124649566.min.css)
    │   ├── fonts.css                Local @font-face for Ovo
    │   └── arabic-font.css          Tajawal @font-face + applies it to all page text
    ├── js/
    │   ├── tilda-fallback-1.0.min.js
    │   ├── tilda-scripts-3.0.min.js
    │   ├── tilda-lazyload-1.0.min.js
    │   ├── tilda-animation-2.0.min.js
    │   ├── tilda-animation-sbs-1.0.min.js
    │   ├── tilda-zero-1.1.min.js
    │   ├── tilda-zero-scale-1.0.min.js
    │   ├── tilda-zero-fixed-1.0.min.js
    │   ├── tilda-popup-1.0.min.js
    │   ├── tilda-forms-1.0.min.js
    │   ├── tilda-events-1.0.min.js
    │   ├── tilda-variant-select-1.0.min.js
    │   ├── tilda-stat-1.0.min.js
    │   └── page.min.js              Per-page bundle (was tilda-blocks-page124649566.min.js)
    ├── fonts/
    │   ├── Ovo-Regular.woff
    │   ├── Ovo-Regular.woff2
    │   ├── GT-Super-Display-Lig.woff
    │   ├── ImperialScript-Regul.woff
    │   └── Tajawal-{400,500,700}-{arabic,latin}.woff2   Arabic webfont
    ├── img/
    │   ├── favicon.ico
    │   ├── Mask_group_2_1_Trace.svg
    │   ├── full/                    Full-size images (webp, used by lazyload data-original)
    │   └── thumb/                   20x lazyload placeholders (png)
    ├── audio/
    │   └── Alex-Warren-Ordinary.mp3
    └── video/
        └── IMG_6230.MP4
```

## How to run

Any static file server works. Pick one:

### Python

```powershell
python -m http.server 8000
```

Then open: <http://localhost:8000/>

### Node (no install)

```powershell
npx serve .
```

### VS Code

Install the *Live Server* extension and click **Go Live** on `index.html`.

## Notes on offline / online behavior

- All HTML, page CSS, page JS, fonts, images, audio and video referenced **directly** by the HTML are now local.
- A small number of font files referenced **inside `page.min.css`** were not part of the original scrape; they still resolve from `static.tildacdn.net` over the network when online, and gracefully fall back to default serif/sans-serif fonts when offline.
- The Tilda statistics script (`tilda-stat-1.0.min.js`) is loaded from `assets/js/`. It will attempt to send anonymous events to Tilda's analytics endpoint when online — disable internet to prevent this.
- DNS-prefetch hints in `<head>` (`ws.tildacdn.com`, `static.tildacdn.net`) are kept as-is; they don't load resources, only resolve DNS.

## What was changed vs. the scraped copy

- **Folder structure** — flattened the host-based mirror into a normal `assets/{css,js,fonts,img,audio,video}/` layout.
- **Filenames** — the per-page bundle was renamed from `tilda-blocks-page124649566.min.*` to `page.min.*`. Optimised images dropped the redundant `.png.webp` suffix to just `.webp`.
- **Paths** — every absolute `https://*.tildacdn.*` / Dropbox URL referenced by HTML or the page CSS was rewritten to a relative path under `assets/`.
- **Nothing else.** No HTML markup, no styles, no scripts, no animations, no design changes.
