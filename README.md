# LLMs Contain Multitudes — companion website

Static companion site for the NeurIPS 2026 Datasets & Benchmarks Track paper
*LLMs Contain Multitudes: How Deployment Context Reshapes Model-Level Preferences and Values*.

## Files

| File | Purpose |
|---|---|
| `index.html` | Page markup, styles, and the cycling-letter animation script. |
| `charts.js` | All chart and table rendering (vanilla JS, no build step, no framework). |
| `site_data.js` | Precomputed statistics consumed by `charts.js`. ~1.3 MB. |
| `assets/cambridge.svg` | University of Cambridge mark used in the footer. |
| `assets/og-preview.png` | 1200x630 social-share card used by Open Graph + Twitter Card. |

No build step, no dependencies. The page loads Google Fonts and Hugging Face dataset link over HTTPS.

## Deploy to GitHub Pages

1. Create a new GitHub repository (e.g. `llm-multitudes-website`).
2. Copy every file in this folder into the repository root and commit.
3. In the repo, go to **Settings → Pages**.
4. Under **Source**, pick the `main` branch and `/ (root)` folder, then save.
5. Wait ~30 seconds; your site appears at `https://<your-username>.github.io/<repo-name>/`.

### After your first deploy: update the social-preview URLs

`index.html` ships with a `REPLACE_ME` placeholder for the share-card URL.
Once your GitHub Pages URL is live, open `index.html`, find the three places
that say `assets/og-preview.png` plus the one `og:url`, and rewrite them as
absolute URLs against your live domain, for example:

```html
<meta property="og:url"   content="https://your-name.github.io/llm-multitudes-website/">
<meta property="og:image" content="https://your-name.github.io/llm-multitudes-website/assets/og-preview.png">
<meta property="og:image:secure_url" content="https://your-name.github.io/llm-multitudes-website/assets/og-preview.png">
<meta name="twitter:image"           content="https://your-name.github.io/llm-multitudes-website/assets/og-preview.png">
```

Why: most modern scrapers (Twitter/X, LinkedIn, Slack, Discord, iMessage)
resolve the relative path against the page, but a couple of older crawlers
still expect an absolute HTTPS URL.

After updating, re-run a fresh scrape:
- Twitter/X: <https://cards-dev.twitter.com/validator>
- Facebook: <https://developers.facebook.com/tools/debug/>
- LinkedIn: <https://www.linkedin.com/post-inspector/>

## Local preview

Any static HTTP server works. From inside this folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Opening `index.html` via `file://` mostly works but a few features (Google Fonts CORS, the cycling-letter animation initialisation) are smoother over HTTP.
