# Core Blueprint Open Source

The static organisation website for [Core Blueprint](https://github.com/Core-Blueprint).

**Positioning:** A small, curated introduction to digital autonomy, engineering principles and publicly accessible source code. Official product, learning and commercial information remains at [coreblueprint.io](https://coreblueprint.io/).

## Architecture

- One semantic `index.html` and one responsive stylesheet, `assets/css/main.css`.
- Full-width sections with `.cb-section__inner` content wrappers and a locally hosted compressed hero image under `assets/images/`.
- Original supplied SVG logo in `assets/brand/core-blueprint-logo.svg`, presented without a background, padding or a card wrapper in both color schemes.
- No JavaScript, framework, generator, CDN, analytics, external font service, GitHub API calls or build step.
- Two local Latin-subset variable WOFF2 fonts: Space Grotesk for headings, buttons, eyebrows and navigation; Inter for content. System fallback covers unsupported glyphs.
- Font binaries are distributed under their own SIL Open Font License 1.1; license texts are in `assets/fonts/licenses/`. Source: [Fontsource font-files](https://github.com/fontsource/font-files/tree/main/fonts/variable), using the Inter and Space Grotesk Google Fonts families.
- System fonts and automatic light/dark presentation using `prefers-color-scheme`.
- Curated project descriptions and links are edited in `index.html`.
- `.nojekyll` disables Jekyll preprocessing.

## Brand styling
- Dark-mode page background: `#07090d`.
- All `h1`–`h3` headings receive a decorative gradient dot via `::after`, blue `#0037ff` to turquoise `#00ffdd`. Keep trailing periods out of heading text.
- Full-width `<section>` elements own their backgrounds and pseudo-elements; each has an inner `.cb-section__inner` that constrains only the content. The hero background is the supplied dashboard composition, optimized to local AVIF. The hero overlay is 60% black (`rgba(0, 0, 0, 0.6)`) over the entire section in both color modes. This is not a separate radial glow.
- Project external-link arrows appear after the heading's decorative dot.

## Hero image asset

The CSS references `assets/images/cb-dashboard-spatial-hero-bg.avif` as a local background. Add the optimized asset to that exact path before testing or publishing. This image is supplied separately as `core-blueprint-hero-asset.zip` because this integration cannot write the binary into the GitHub repository directly.

From the repository root, after downloading the image asset ZIP:

```bash
unzip -o ~/Downloads/core-blueprint-hero-asset.zip -d .
test -s assets/images/cb-dashboard-spatial-hero-bg.avif
sha256sum assets/images/cb-dashboard-spatial-hero-bg.avif
```

Expected SHA-256: `c966845843a1b62484a7d22b9a17b9d3587cb42ff48776e27a9df6c423e39052`.

The source image is 1672 × 941 pixels; the optimized AVIF is approximately 43 KB. The 60% black hero overlay covers the full viewport, while `.cb-section__inner` constrains only the copy and controls.

## Local preview

From the repository root:

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080`. Confirm the hero photo and `::before` cover the full browser width, while content follows the container width. Check the mobile photo crop, the original logo, locally loaded fonts, keyboard navigation, both color modes, mobile layouts and outbound links before accepting any changes. In browser DevTools → Network, confirm the two WOFF2 requests and SVG come from localhost and that there are no third-party requests.

## Optional offline release archive

GitHub Pages publishes the source directly, so no build is required. For review or a snapshot of the site:

```bash
mkdir -p dist
python3 -m zipfile -c dist/core-blueprint-github-pages.zip index.html assets .nojekyll
python3 -m zipfile -t dist/core-blueprint-github-pages.zip
sha256sum dist/core-blueprint-github-pages.zip
```

`dist/` is ignored by Git.

## Publishing policy

**Do not enable GitHub Pages, change repository visibility, merge the website branch, or configure a custom domain without explicit approval.**

When accepted, merge the approved branch to `main`, make the repository public if required by the organisation's GitHub plan, then choose **Settings → Pages → Deploy from a branch → main / (root)**. GitHub Pages will perform its own managed deployment. No custom Actions workflow is necessary.

Review publication settings and the repository contents before making the repository public. Published Pages content is public even when the underlying repository is private on eligible plans.
