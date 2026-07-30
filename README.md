# SciComm Initiative — Website

A clean, fully static website for a science communication group. No frameworks, no build tools — just HTML, CSS, and a little vanilla JavaScript.

## Pages

| File | Description |
|---|---|
| `index.html` | Homepage with hero, featured posts, podcast preview, Science Café teaser |
| `blog.html` | Blog listing with category filter |
| `podcast.html` | Episode list for "The Curious Lab" podcast |
| `workshops.html` | Upcoming and past workshop listings |
| `cafe.html` | Science Café page with next event, RSVP form, and past topics |
| `about.html` | Team, values, get-involved, and contact form |
| `style.css` | All shared styles |

## Hosting on GitHub Pages

1. **Create a new GitHub repository** (e.g. `scicomm-Initiative`)

2. **Upload all files** — drag and drop into the repository, or use git:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git remote add origin https://github.com/YOUR-USERNAME/scicomm-collective.git
   git push -u origin main
   ```

3. **Enable GitHub Pages**:
   - Go to your repo → **Settings** → **Pages**
   - Under "Source", select **Deploy from a branch**
   - Choose **main** branch, **/ (root)** folder
   - Click **Save**

4. Your site will be live at `https://YOUR-USERNAME.github.io/scicomm-initiative/` within a few minutes.

## Custom domain (optional)

To use a custom domain like `scicomm-initiative.org`:
1. Buy a domain from any registrar (Namecheap, Google Domains, etc.)
2. Add a file called `CNAME` to this repo containing just your domain: `scicomm-initiative.org`
3. In your domain registrar's DNS settings, add a CNAME record pointing to `YOUR-USERNAME.github.io`

## Customising the content

- **Colours**: all defined as CSS variables at the top of `style.css`
- **Fonts**: loaded from Google Fonts — swap out `Lora` and `DM Sans` for any pairing you prefer
- **Team / posts / episodes**: edit the HTML directly — each card is clearly commented
- **RSVP / Contact forms**: currently show a confirmation message on click. For real form submissions, connect to [Formspree](https://formspree.io) (free tier available) by replacing the button `onclick` with a proper `<form action="https://formspree.io/f/YOUR-ID" method="POST">`

## Adding a blog post

Copy any `<article class="blog-card">` block in `blog.html` and fill in your own content. For a full Markdown-based blog with automatic listings, consider migrating to [Quarto](https://quarto.org) — the CSS design will carry over with minor tweaks.

## Migrating to Quarto

This site was designed to be a starting point. When you're ready to scale up:
- Install Quarto and run `quarto create project website`
- Copy `style.css` into `assets/` and reference it from `_quarto.yml`
- Convert each `.html` page to a `.qmd` file — content ports directly
- Quarto handles blog listings, RSS feeds, and search automatically

---

Built with plain HTML · Hosted free on GitHub Pages
