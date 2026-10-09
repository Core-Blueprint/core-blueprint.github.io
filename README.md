# Core Blueprint Open Source

The static organisation website for [Core Blueprint](https://github.com/Core-Blueprint).

**Positioning:** A small, curated introduction to digital autonomy, engineering principles and publicly accessible source code. Official product, learning and commercial information remains at [coreblueprint.io](https://coreblueprint.io/).

## Architecture

- One semantic `index.html` and one responsive stylesheet, `assets/css/main.css`.
- No JavaScript, framework, generator, CDN, analytics, font service, GitHub API calls or build step.
- System fonts and automatic light/dark presentation using `prefers-color-scheme`.
- Curated project descriptions and links are edited in `index.html`.
- `.nojekyll` disables Jekyll preprocessing.

## Local preview

From the repository root:

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080`. Review keyboard navigation, light/dark appearance, mobile layouts and outbound links before accepting any changes.

## Optional offline release archive

GitHub Pages publishes the source directly, so no build is required. For review or a snapshot of the site:

```bash
mkdir -p dist
python3 -m zipfile -c dist/core-blueprint-github-pages.zip index.html assets/css/main.css .nojekyll
python3 -m zipfile -t dist/core-blueprint-github-pages.zip
sha256sum dist/core-blueprint-github-pages.zip
```

`dist/` is ignored by Git.

## Publishing policy

**Do not enable GitHub Pages, change repository visibility, merge the website branch, or configure a custom domain without explicit approval.**

When accepted, merge the approved branch to `main`, make the repository public if required by the organisation's GitHub plan, then choose **Settings → Pages → Deploy from a branch → main / (root)**. GitHub Pages will perform its own managed deployment. No custom Actions workflow is necessary.

Review publication settings and the repository contents before making the repository public. Published Pages content is public even when the underlying repository is private on eligible plans.
