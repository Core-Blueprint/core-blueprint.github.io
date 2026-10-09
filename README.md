# Core Blueprint Open Source

The static organisation website for [Core Blueprint](https://github.com/Core-Blueprint).

**Positioning:** A small, curated introduction to digital autonomy, engineering principles and publicly accessible source code. Official product, learning and commercial information remains at [coreblueprint.io](https://coreblueprint.io/).

## Architecture

- One semantic `index.html` and one responsive stylesheet, `assets/css/main.css`.
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
- The hero has a `::before` overlay matching the supplied linear-gradient snippet. Since the production token `--cf-dark-60` was not provided, the fallback is transparent. The true radial glow still needs the original CSS; do not invent a substitute.
- Project external-link arrows appear after the heading's decorative dot.

## Local preview

From the repository root:

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080`. Review the original logo, locally loaded fonts, keyboard navigation, light/dark appearance, mobile layouts and outbound links before accepting any changes. In browser DevTools → Network, confirm the two WOFF2 requests and SVG come from localhost and that there are no third-party requests.

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
