# SciComm Collective — Quarto Website

This is the SciComm Collective website converted from plain HTML to [Quarto](https://quarto.org).

## File structure

```
_quarto.yml          ← Site config: navbar, footer, theme, CSS
index.qmd            ← Homepage
blog.qmd             ← Blog listing with category filter
podcast.qmd          ← Podcast episode list
workshops.qmd        ← Workshop listings
cafe.qmd             ← Science Café page with RSVP form
about.qmd            ← Team, values, contact form
style.css            ← All custom styles (carried over from original site)
quarto-overrides.css ← Suppresses Quarto default chrome that clashes with custom design
```

## Prerequisites

Install Quarto from https://quarto.org/docs/get-started/ (free, available for macOS, Windows, Linux).

## Preview locally

```bash
quarto preview
```

This starts a local dev server at `http://localhost:4848` with live reload.

## Build for production

```bash
quarto render
```

Output goes to `_site/`. Upload that folder to any static host.

## Deploy to GitHub Pages

1. Create a GitHub repository and push all files.
2. Go to **Settings → Pages**, set source to **GitHub Actions**.
3. Create `.github/workflows/publish.yml`:

```yaml
name: Publish to GitHub Pages
on:
  push:
    branches: [main]
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Your site will be live at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

## How `.qmd` files work

Each page is a Quarto Markdown file with a YAML frontmatter block (`---`) followed by content.
Because all the page content is HTML (not Markdown prose), the files work identically to the original `.html` files — Quarto passes raw HTML through unchanged.

Key frontmatter options used here:
- `page-layout: full` — removes Quarto's default centred column, allowing full-bleed sections
- `toc: false` — hides the automatic table of contents
- `include-in-header` — injects page-specific `<style>` blocks (used in `about.qmd`)

## Adding JavaScript

Inline `<script>` tags must be wrapped in a raw HTML block so Quarto doesn't escape them:

````
```{=html}
<script>
  // your JS here
</script>
```
````

This is already done for the filter, RSVP, and contact form scripts.

## Connecting real forms

The RSVP and contact forms currently show a confirmation on click.
To wire them to a real backend, replace the `onclick` handler with [Formspree](https://formspree.io):

```html
<form action="https://formspree.io/f/YOUR-ID" method="POST">
  ...
  <button type="submit" class="btn btn-teal">Send →</button>
</form>
```

## Migrating blog posts to native Quarto listings

Right now, blog posts are hand-coded HTML cards in `blog.qmd`.
To get automatic listings, RSS, and pagination, create individual post files:

```
posts/
  2025-04-28-ants-engineers/index.qmd
  2025-04-14-music-chills/index.qmd
  ...
```

Then replace the hand-coded grid in `blog.qmd` with:

```yaml
listing:
  contents: posts
  type: grid
  sort: "date desc"
  categories: true
```

See https://quarto.org/docs/websites/website-listings.html for full docs.
