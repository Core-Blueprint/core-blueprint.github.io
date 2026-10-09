# Core Blueprint Open Source

The static organisation website for [Core Blueprint](https://github.com/Core-Blueprint).

**Positioning:** A small, curated introduction to digital autonomy, engineering principles and publicly accessible source code. Official product, learning and commercial information remains at [coreblueprint.io](https://coreblueprint.io/).

## Architecture

- One semantic `index.html` and one responsive stylesheet, `assets/css/main.css`.
- Full-width sections with `.cb-section__inner` content wrappers and a locally hosted PNG hero image under `assets/images/`.
- Original supplied SVG logo in `assets/brand/core-blueprint-logo.svg`, presented without a background, padding or a card wrapper in both color schemes.
- No JavaScript, framework, generator, CDN, analytics, external font service, GitHub API calls or build step.
- Two local Latin-subset variable WOFF2 fonts: Space Grotesk for headings, buttons, eyebrows and navigation; Inter for content. System fallback covers unsupported glyphs.
- Font binaries are distributed under their own SIL Open Font License 1.1; license texts are in `assets/fonts/licenses/`. Source: [Fontsource font-files](https://github.com/fontsource/font-files/tree/main/fonts/variable), using the Inter and Space Grotesk Google Fonts families.
- Fixed brand palette independent of system appearance: header, hero, CTA and footer are dark; reading sections alternate between white and a 5%-opacity primary-blue tint, always with dark text.
- Curated project descriptions and links are edited in `index.html`.
- `.nojekyll` disables Jekyll preprocessing.

## Brand styling
- Header, hero, CTA and footer background: `#07090d`. Light content sections: white (`#fff`) with dark text, alternating with the reusable `.section--tinted` class and `--cf-primary-5: rgba(0, 55, 255, 0.05)` (equivalent to `#f2f5ff` over white). Currently Principles is white and Projects is tinted.
- All `h1`–`h3` headings remain a single foreground color and receive a decorative gradient dot via `::after`, blue `#0037ff` to turquoise `#00ffdd`. Cyan must not be used as a standalone text, link, or focus color. Keep trailing periods out of heading text.
- Eyebrows use Space Grotesk, uppercase text, 0.1rem tracking, weight 500, small rounded corners, and a 20%-opacity primary-blue background (`rgba(0, 55, 255, 0.2)`). Padding and font size are provisional local mappings until source-site spacing tokens are provided.
- Number labels use reduced opacity on the inherited text color rather than a cyan accent.
- Full-width `<section>` elements own their backgrounds and pseudo-elements; each has an inner `.cb-section__inner` that constrains only the content. The hero background is the supplied dashboard composition, provided as the original PNG without format conversion. The hero overlay is 60% black (`rgba(0, 0, 0, 0.6)`) over the entire section in both color modes. This is not a separate radial glow.
- Project external-link arrows appear after the heading's decorative dot.

## Hero image asset

The CSS references `assets/images/cb-dashboard-spatial-hero-bg.png`. Keep the original user-supplied PNG format and basename; do not convert the asset to AVIF or require a separate ZIP download.

From the repository root, using the PNG already in the user's Downloads folder:

```bash
test -s "$HOME/Downloads/cb-dashboard-spatial-hero-bg.png"
install -Dm644 "$HOME/Downloads/cb-dashboard-spatial-hero-bg.png" assets/images/cb-dashboard-spatial-hero-bg.png
file assets/images/cb-dashboard-spatial-hero-bg.png
sha256sum assets/images/cb-dashboard-spatial-hero-bg.png
```

The verified upload is a 1672 × 941 RGBA PNG. Its SHA-256 is `e6122fd45ed267024a2d36e0c169cda8995eaad33c2824688dcae47349f2e2b3`. The full-width hero retains a black overlay at 60% opacity; the `.cb-section__inner` wrapper only constrains text content.

## Local preview

From the repository root:

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080`. Confirm the hero photo and `::before` cover the full browser width, while content follows the container width. Check the mobile photo crop, the original logo, locally loaded fonts, keyboard navigation, dark framing versus white content in both system appearance modes, mobile layouts and outbound links before accepting any changes. In browser DevTools → Network, confirm the two WOFF2 requests and SVG come from localhost and that there are no third-party requests.

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
