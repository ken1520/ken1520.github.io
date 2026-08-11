# ken1520.github.io

My CV and portfolio, served at **https://ken1520.github.io**.

One self-contained static HTML file. No build step, no dependencies, no external requests —
both typefaces (Archivo and IBM Plex Mono) are inlined as base64 woff2, so the page renders
identically offline and can't fall back to a system font if a CDN is slow or blocked.

## Editing

Everything lives in `index.html`. The content sits in plain semantic markup near the bottom
of the file; the design tokens sit in the `:root` block near the top, after the `@font-face`
rules.

To change the palette, edit the tokens rather than the components — they're redefined in four
places that must stay in sync:

| Block | Purpose |
|---|---|
| `:root` | light theme |
| `@media (prefers-color-scheme: dark)` | follows the OS setting |
| `:root[data-theme="dark"]` / `:root[data-theme="light"]` | the on-page toggle, which must beat the media query in both directions |
| `@media print` | forces a light, ink-friendly palette |

### Career track bars

Each role's rail shows where that job sits in the overall career span. The bar reads its
position from two inline custom properties, in months from **2019 Jun**, over a total span
of **86** months:

```html
<div class="tenure" style="--from: 72; --span: 14" data-current="true" aria-hidden="true"></div>
```

When adding a role or when the current job passes another month boundary, update `--from`
and `--span` on the affected entries and the `86` divisor in the `.tenure::before` rule,
otherwise the segments stop tiling the track correctly.

## Checks worth repeating after edits

- Contrast: the light theme is where this breaks. Every text token needs 4.5:1 against its
  ground — `--ink-3` carries most of the small metadata and sits closest to the line.
- Print: the page is expected to export cleanly to PDF, since recruiters do that.
- Responsive: the role grid collapses at 40rem, projects and skills at 46rem.

## Deployment

GitHub Pages serves `main` at the repository root. Pushing to `main` publishes.
`.nojekyll` disables Jekyll processing, which this page doesn't need.
